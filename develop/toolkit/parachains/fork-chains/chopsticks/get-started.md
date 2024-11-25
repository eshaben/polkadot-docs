---
title: Get Started
description: Simplify Polkadot SDK development with Chopsticks. Learn essential features, how to install Chopsticks, and how to configure local blockchain forks.
---

# Get Started

## Introduction

[Chopsticks](https://github.com/AcalaNetwork/chopsticks/){target=\_blank}, developed by the [Acala Foundation](https://github.com/AcalaNetwork){target=\_blank}, is a versatile tool tailored for developers working on Polkadot SDK-based blockchains. With Chopsticks, you can fork live chains locally, replay blocks to analyze extrinsics, and simulate complex scenarios like XCM interactions all without deploying to a live network.

This guide walks you through installing Chopsticks and provides information on configuring a local blockchain fork. By streamlining testing and experimentation, Chopsticks empowers developers to innovate and accelerate their blockchain projects within the Polkadot ecosystem.

For additional support and information, please reach out through [GitHub Issues](https://github.com/AcalaNetwork/chopsticks/issues){target=_blank}.

!!! note
    Chopsticks uses [Smoldot](https://github.com/smol-dot/smoldot){target=_blank} light client, which only supports the native Polkadot SDK API. Consequently, a Chopsticks-based fork doesn't support Ethereum JSON-RPC calls, meaning you cannot use it to fork your chain and connect Metamask.

## Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/en/){target=\_blank}
- A package manager such as [npm](https://www.npmjs.com/){target=\_blank}, which should be installed with Node.js by default, or [Yarn](https://yarnpkg.com/){target=\_blank}

## Install Chopsticks

You can install Chopsticks globally or locally in your project. Choose the option that best fits your development workflow.

!!! note
    This documentation explains the features of Chopsticks version `{{ dependencies.chopsticks.version }}`. Make sure you're using the correct version to match these instructions.

### Global Installation

To install Chopsticks globally, allowing you to use it across multiple projects, run:

```bash
npm i -g @acala-network/chopsticks@{{ dependencies.chopsticks.version }}
```

Now, you should be able to run the `chopsticks` command from your terminal.

### Local Installation

To use Chopsticks in a specific project, first create a new directory and initialize a Node.js project:

```bash
mkdir my-chopsticks-project
cd my-chopsticks-project
npm init -y
```

Then, install Chopsticks as a local dependency:

```bash
npm i @acala-network/chopsticks@{{ dependencies.chopsticks.version }}
```

Finally, you can run Chopsticks using the `npx` command:

```bash
npx @acala-network/chopsticks
```

## Configure Chopsticks

To run Chopsticks, you need to configure some parameters. This can be set either through using a configuration file or the command line interface (CLI). The parameters that can be configured are as follows:

- `genesis` - the link to a parachain's raw genesis file to build the fork from, instead of an endpoint
- `timestamp` - timestamp of the block to fork from
- `endpoint` - the endpoint of the parachain to fork
- `block` - use to specify at which block hash or number to replay the fork
- `wasm-override` - path of the Wasm to use as the parachain runtime, instead of an endpoint's runtime
- `db` - path to the name of the file that stores or will store the parachain's database
- `config` - path or URL of the config file
- `port` - the port to expose an endpoint on
- `build-block-mode` - how blocks should be built in the fork: batch, manual, instant
- `import-storage` - a pre-defined JSON/YAML storage path to override in the parachain's storage
- `allow-unresolved-imports` - whether to allow Wasm unresolved imports when using a Wasm to build the parachain
- `html` - include to generate storage diff preview between blocks
- `mock-signature-host` - mock signature host so that any signature starts with `0xdeadbeef` and filled by `0xcd` is considered valid

### Configuration File

The Chopsticks source repository includes a collection of [YAML](https://yaml.org/){target=\_blank} files that can be used to set up various Polkadot SDK chains locally. You can download these configuration files from the [repository's `configs` folder](https://github.com/AcalaNetwork/chopsticks/tree/master/configs){target=\_blank}.

An example of a configuration file for Polkadot is as follows:

```yaml
--8<-- 'code/develop/toolkit/parachains/fork-chains/chopsticks/get-started/example-config.yml'
```

The configuration file allows you to modify the storage of the forked network by rewriting the pallet, state component and value that you want to change. For example, Polkadot's file rewrites Alice's `system.Account` storage so that the free balance is set to `10000000000000000000`.

### CLI Flags

Alternatively, all settings (except for genesis and timestamp) can be configured via command-line flags, providing a comprehensive method to set up the environment. 

## Where to Go Next

- Visit the [Fork a Chain with Chopsticks](/tutorials/polkadot-sdk/testing/fork-live-chains/){target=\_blank} guide for step-by-step instructions for configuring and interacting with your forked chain.