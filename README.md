# AWS SLS Auctions

A small AWS service built with the [Serverless Framework](https://www.serverless.com/). The project is split into independent services that can be deployed separately.

## Monorepo

The project uses [pnpm workspaces](https://pnpm.io/workspaces) as a monorepo:

```text
services/
  auctions/
  notifications/
packages/
  shared/
```

The `services` directory contains the individual Serverless services. The `packages` directory contains shared code used by multiple services.

## Installing dependencies

After cloning the project, install all dependencies from the monorepo root:

```sh
pnpm install
```

Install shared development tools, such as Serverless Framework, ESLint, or Prettier, in the workspace root:

```sh
pnpm add -Dw serverless
pnpm add -Dw eslint prettier
```

Install a dependency used by only one service directly in that service:

```sh
pnpm --filter auctions add @aws-sdk/client-dynamodb
pnpm --filter notifications add @aws-sdk/client-sns
```

Add an internal shared package as a workspace dependency:

```sh
pnpm --filter auctions add @aws-sls-auctions/shared@workspace:*
```

`pnpm add -Dw` adds a dependency to the workspace root as a development dependency. `pnpm --filter <name> add` adds a dependency only to the selected package or service.

## Scripts

Format the entire monorepo:

```sh
pnpm format
```

Run ESLint:

```sh
pnpm lint
```

Deploy an individual service:

```sh
pnpm --filter auctions deploy
pnpm --filter notifications deploy
```
