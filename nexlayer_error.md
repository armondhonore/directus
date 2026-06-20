# Nexlayer Build Failure Report

**Pipeline:** 19ee7006bc9
**Repository:** https://github.com/armondhonore/directus
**Error category:** 
**Error summary:** pipeline: wait for pod: runner container for job pipeline-19ee7006-fix6 not running within 6m0s

## Build log
```

```

## Repository build artifacts

These are the actual files from the repository. Use these to understand how the project
is SUPPOSED to be built — do not rely solely on the broken Dockerfile below.


### package.json
```
{
	"name": "directus-monorepo",
	"private": true,
	"homepage": "https://directus.com",
	"type": "module",
	"scripts": {
		"build": "pnpm --recursive run build",
		"format": "prettier --cache --check .",
		"lint": "eslint --cache .",
		"lint:style": "stylelint '**/*.{css,scss,vue}' --ignore-path .gitignore --cache",
		"test": "pnpm --recursive --filter '!tests-blackbox' test",
		"test:blackbox": "rimraf ./dist && pnpm --filter directus deploy --legacy --prod dist && pnpm --filter tests-blackbox test",
		"test:coverage": "pnpm --recursive --filter '!tests-blackbox' test:coverage"
	},
	"devDependencies": {
		"@changesets/cli": "catalog:",
		"@directus/release-notes-generator": "workspace:*",
		"@eslint/js": "catalog:",
		"eslint": "catalog:",
		"eslint-config-prettier": "catalog:",
		"eslint-plugin-import": "catalog:",
		"eslint-plugin-vue": "catalog:",
		"globals": "catalog:",
		"postcss-html": "catalog:",
		"prettier": "catalog:",
		"rimraf": "catalog:",
		"stylelint": "catalog:",
		"stylelint-config-standard": "catalog:",
		"stylelint-config-standard-scss": "catalog:",
		"stylelint-config-standard-vue": "catalog:",
		"stylelint-use-logical": "catalog:",
		"typescript": "catalog:",
		"typescript-eslint": "catalog:"
	},
	"pnpm": {
		"overrides": {
			"@directus/license>@directus/types": "workspace:*",
			"fast-xml-parser": "5.8.0",
			"@yarnpkg/shell>cross-spawn": "7.0.6",
			"tar": "7.5.15",
			"qs": "6.15.2",
			"minimatch@10": "10.2.5",
			"minimatch@9": "9.0.9",
			"basic-ftp": "5.3.1",
			"underscore": "1.13.8",
			"flatted": "3.4.2",
			"express@4>path-to-regexp": "0.1.13",
			"micromatch>picomatch": "2.3.2",
			"anymatch>picomatch": "2.3.2",
			"picomatch": "4.0.4",
			"defu": "6.1.7",
			"unplugin-vue>vite": "8.0.14",
			"vitest@3>vite": "7.3.2",
			"protobufjs": "7.5.6",
			"js-beautify>js-cookie": "3.0.7",
			"pm2-sysmonit>systeminformation": "5.31.6",
			"ajv>fast-uri": "3.1.2",
			"braintrust>simple-git": "3.36.0",
			"launch-editor>shell-quote": "1.8.4"
	
... (truncated)
```

### docker-compose.yml
```
# This compose file is meant to spin up a copy of supported database vendors,
# Redis, S3 (Minio) and a fake SMTP server (MailDev).
#
# ONLY FOR DEBUGGING. THIS IS NOT INTENDED FOR PRODUCTION USE.
#
# For production use see the docker compose file example in the docs:
#     https://docs.directus.com/self-hosted/docker-guide.html#example-docker-compose
#
# For receiving emails via MailDev, you'll need to add the following to your env:
#   EMAIL_FROM=directus@directus.io
#   EMAIL_TRANSPORT=smtp
#   EMAIL_SMTP_HOST=0.0.0.0
#   EMAIL_SMTP_PORT=1025
#
# Ports:
#   Maildev SMTP:    1025
#   Maildev Web-UI:  1080
#   Postgres:        5100
#   MySQL (8):       5101
#   MariaDB:         5102
#   MS SQL:          5103
#   Oracle:          5104
#   Redis:           5105
#   Minio (S3):      5106
#   Azure            5107
#   MySQL (5.7):     5108
#   Keycloak:        5110
#   Postgres (10):   5111
#   Minio Admin:     5112
#   CockroachDB:     5113
#
# Credentials:
#   Postgres:
#     User:          postgres
#     Password:      secret
#
#   MySQL:
#     User:          root
#     Password:      secret
#
#   MariaDB:
#     User:          root
#     Password:      secret
#
#   MS SQL:
#     User:          sa
#     Password:      Test@123
#
#   Oracle DB:
#     User:          secretsysuser
#     Password:      secretpassword
#     Role:          SYSDEFAULT
#     SID:           XE
#
#   Redis:
#     n/a
#
#   Minio:
#     Key:           minioadmin
#     Secret:        minioadmin
#     (Make sure to set S3_FORCE_PATH_STYLE to true)
#
#   Azure Blob Storage
#     Name:          devstoreaccount1
#     Key:           Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
#     Container:     devstoreaccount1
#
#   Keycloak
#     User:          admin
#     Password:      secret
#
#   CockroachDB
#     User:          admin
#     Password:      --

version: '3.8'

services:
  postgres:
    image: postgis/postgis:13-3.4-alpine
    environment:
      POST
... (truncated)
```

### pnpm-workspace.yaml
```
packages:
  - directus
  - app
  - api
  - sdk
  - packages/*
  - tests/*

catalog:
  '@ai-sdk/anthropic': 3.0.58
  '@ai-sdk/devtools': 0.0.15
  '@ai-sdk/google': 3.0.43
  '@ai-sdk/openai': 3.0.41
  '@ai-sdk/openai-compatible': 2.0.35
  '@ai-sdk/vue': 3.0.116
  '@authenio/samlify-node-xmllint': 2.0.0
  '@aws-sdk/client-s3': 3.928.0
  '@aws-sdk/client-sesv2': 3.928.0
  '@aws-sdk/lib-storage': 3.928.0
  '@azure/storage-blob': 12.29.1
  '@braintrust/otel': 0.2.0
  '@changesets/cli': 2.29.7
  '@changesets/get-github-info': 0.6.0
  '@changesets/types': 6.1.0
  '@directus/errors': 2.3.1
  '@directus/license': 0.2.0
  '@directus/schema-builder': workspace:*
  '@directus/tsconfig': 4.0.0
  '@directus/types': workspace:*
  '@directus/vue-split-panel': 0.8.9
  '@editorjs/attaches': 1.3.2
  '@editorjs/checklist': 1.6.0
  '@editorjs/code': 2.9.3
  '@editorjs/delimiter': 1.4.2
  '@editorjs/editorjs': 2.31.2
  '@editorjs/embed': 2.7.6
  '@editorjs/header': 2.8.8
  '@editorjs/image': 2.10.3
  '@editorjs/inline-code': 1.5.2
  '@editorjs/nested-list': 1.4.3
  '@editorjs/paragraph': 2.11.7
  '@editorjs/quote': 2.7.6
  '@editorjs/raw': 2.5.1
  '@editorjs/table': 2.4.5
  '@editorjs/underline': 1.2.1
  '@eslint/js': 9.39.1
  '@fastify/type-provider-typebox': 6.1.0
  '@fortawesome/fontawesome-svg-core': 6.7.2
  '@fortawesome/free-brands-svg-icons': 6.7.2
  '@fullcalendar/core': 6.1.19
  '@fullcalendar/daygrid': 6.1.19
  '@fullcalendar/interaction': 6.1.19
  '@fullcalendar/list': 6.1.19
  '@fullcalendar/timegrid': 6.1.19
  '@godaddy/terminus': 4.12.1
  '@google-cloud/storage': 7.18.0
  '@histoire/plugin-vue': 0.17.17
  '@internationalized/date': 3.10.1
  '@joeattardi/emoji-button': 4.6.4
  '@json2csv/plainjs': 7.0.6
  '@keyv/redis': 3.0.1
  '@langfuse/otel': 4.0.0
  '@mapbox/mapbox-gl-draw': 1.5.1
  '@mapbox/mapbox-gl-draw-static-mode': 1.0.1
  '@mapbox/mapbox-gl-geocoder': 5.1.2
  '@modelcontextprotocol/sdk': 1.29.0
  '@netlify/api': 14.0.14
  '@ngneat/falso': 8.0.2
  '@npm/types': 2.1.0
... (truncated)
```


## Last attempted Dockerfile
```dockerfile
FROM mirror.gcr.io/library/node:22-slim

# Install build essentials for native modules (sqlite3, etc)
RUN apt-get update && apt-get install -y python3 make g++ build-essential && rm -rf /var/lib/apt/lists/*

# Install pnpm using corepack as per packageManager field
RUN npm install -g corepack@latest && corepack enable && corepack prepare pnpm@10.27.0 --activate

WORKDIR /repo

# Copy the entire repository to avoid workspace resolution errors in pnpm v10
COPY . .

# Install dependencies - using --no-frozen-lockfile as per Nexlayer pnpm v10 guidelines
# pnpm v10 requires full context for workspace:* dependencies
RUN pnpm install --no-frozen-lockfile

# Set memory limit for heavy build process
ENV NODE_OPTIONS="--max-old-space-size=8192"

# Build the monorepo
RUN pnpm run build

# Deploy the 'directus' package to the dist folder for runtime
RUN pnpm --filter directus deploy --legacy --prod dist

# Set runtime environment variables
ENV NODE_ENV="production"
ENV PORT=8055
ENV HOSTNAME="0.0.0.0"
ENV DB_CLIENT="sqlite3"
ENV DB_FILENAME="/repo/dist/database/database.sqlite"

# Create necessary runtime directories
RUN mkdir -p dist/database dist/extensions dist/uploads

WORKDIR /repo/dist

EXPOSE 8055

# Bootstrapping the DB before starting the server
CMD ["sh", "-c", "node cli.js bootstrap && node index.js"]

```

## Last attempted nexlayer.yaml
```yaml
application:
  name: directus
  pods:
    - name: app
      image: "# filled by pipeline"
      servicePorts:
        - 8055
      vars:
        NODE_ENV: "production"
        PORT: "8055"
        HOSTNAME: "0.0.0.0"
        DB_CLIENT: "sqlite3"
        DB_FILENAME: "/repo/dist/database/database.sqlite"
```

## Instructions for frontier model

CRITICAL: Before writing any fix, read the repository build artifacts above and answer:
1. What language/runtime does this project use? (go.mod, package.json, pom.xml, Cargo.toml, requirements.txt)
2. What is the actual build command? (package.json scripts.build, Makefile targets, pom.xml goals, gradle tasks)
3. What is the actual start command? (package.json scripts.start, Makefile run target, Procfile)
4. What port does it serve? (EXPOSE, ENV PORT=, --port flag, framework default)
5. What dependencies does it need at runtime? (docker-compose.yml services, .env.example vars)

Then create a correct Dockerfile from scratch based on your analysis:
- All FROM base images must be standard public images (library/, gcr.io, ghcr.io, etc.)
- Use `mirror.gcr.io/library/` prefix for Docker Hub official images (node:*, python:*, golang:*, etc.)
- DO NOT copy broken steps from the "last attempted Dockerfile" — build from what the repo actually needs

Fix nexlayer.yaml if needed:
- Inter-pod service references MUST use `<podName>.pod:<port>` addressing (resolved by the platform via DNS at deploy time)
- Example: `DATABASE_URL: postgresql://user:pass@postgres.pod:5432/db`

Create a file named `nexlayer_fix.md` on THIS branch (`nexlayer`) with this structure:

---
# Nexlayer Fix

## Fixed Dockerfile
```dockerfile
<your fixed Dockerfile>
```

## Fixed nexlayer.yaml
```yaml
<your fixed nexlayer.yaml>
```

## Notes
<explain: what build command you found, what was wrong with the previous Dockerfile, what you changed and why>
---

Nexlayer detects `nexlayer_fix.md` on the next pipeline run and applies your fixes automatically.
