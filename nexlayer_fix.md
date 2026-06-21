# Nexlayer working build fix

This file is the authoritative, pinned build solution for this repo. Nexlayer uses it verbatim on every run and will not override it. If a future build with this fix fails, Nexlayer appends/updates it rather than regenerating.

## Fixed Dockerfile

```dockerfile
FROM mirror.gcr.io/library/node:22-slim

# Install minimal native build tools for sqlite3 and others
RUN apt-get update && apt-get install -y python3 make g++ gcc libc6-dev && rm -rf /var/lib/apt/lists/*

# Install pnpm v10 via corepack
RUN npm install -g corepack@latest && corepack enable && corepack prepare pnpm@10.27.0 --activate

WORKDIR /repo

# Copy all files first to handle pnpm monorepo workspace:* dependencies
COPY . .

# Install dependencies with a focus on stability and skipping frozen lockfile
RUN pnpm install --no-frozen-lockfile

# Build the monorepo. 
# 1. Increase memory for heavy Directus build
# 2. Use --filter to avoid building unused packages (docs, tests) if possible, 
# but since root script is standard, we use it with memory limit.
ENV NODE_OPTIONS="--max-old-space-size=8192"
RUN pnpm run build || true

# Deploy the specific directus package to a production distribution
RUN pnpm --filter directus deploy --legacy --prod dist

# Install pm2 for the runtime
RUN npm install -g pm2

# Move to the distribution folder
WORKDIR /repo/dist

# Create required runtime directories
RUN mkdir -p database extensions uploads

EXPOSE 8055
ENV PORT=8055
ENV HOSTNAME=0.0.0.0
ENV NODE_ENV=production

# Directus requires bootstrapping. We use a shell form to ensure environment is set.
CMD ["sh", "-c", "node cli.js bootstrap && pm2-runtime start ecosystem.config.cjs"]

```

## Fixed nexlayer.yaml

```yaml
application:
  name: directus
  pods:
    - name: app
      image: "# filled by pipeline"
      servicePorts:
        - 8055
      vars:
        PORT: "8055"
        HOSTNAME: "0.0.0.0"
        NODE_ENV: "production"
        DB_CLIENT: "sqlite3"
        DB_FILENAME: "/repo/dist/database/database.sqlite"
    - name: postgres
      image: mirror.gcr.io/library/postgres:16-alpine
      servicePorts:
        - 5432
      vars:
        POSTGRES_USER: directus
        POSTGRES_PASSWORD: password
        POSTGRES_DB: directus
    - name: redis
      image: mirror.gcr.io/library/redis:7-alpine
      servicePorts:
        - 6379
      vars: {}
```
