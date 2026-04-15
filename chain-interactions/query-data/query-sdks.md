---
title: Query On-Chain State with SDKs
description: "Query on-chain storage (System.Account balances, Assets pallet metadata) on Polkadot Hub using PAPI (`polkadot-api`), Polkadot.js API (`@polkadot/api`, maintenance mode — prefer PAPI or Dedot for new projects), Dedot, Python Substrate Interface (`substrate-interface`), or Subxt (Rust). Covers both account balance and asset information queries with runnable code examples. Requires Node.js 18+, Python 3.8+, or Rust stable toolchain depending on SDK."
categories: Chain Interactions, Tooling
category: Chain Interactions
url: /chain-interactions/query-data/query-sdks/
related:
  - /chain-interactions/query-data/runtime-api-calls/
  - /chain-interactions/query-data/query-rest/
  - /chain-interactions/send-transactions/with-sdks/
page_badges:
  test_workflow: polkadot-docs-query-sdks
page_tests:
  path: polkadot-docs/chain-interactions/query-sdks/tests/docs.test.ts
---

Covers: PAPI (polkadot-api), Polkadot.js API (@polkadot/api), Dedot, Python Substrate Interface (substrate-interface), Subxt, System.Account storage queries, Assets pallet metadata queries
Requires: Node.js 18+ with npm/pnpm/yarn (PAPI, Polkadot.js, Dedot), Python 3.8+ with pip (PSI), or Rust stable with Cargo (Subxt); WebSocket endpoint for Polkadot Hub
Returns: Native token balance (free, reserved, frozen) and asset metadata including name, symbol, decimals, and account asset balance

# Query On-Chain State with SDKs

## Query On-Chain Data

=== "PAPI"

    **Prerequisites**

    - [Node.js](https://nodejs.org/){target=\_blank} v18 or higher
    - npm, pnpm, or yarn package manager

    **Environment Setup**

    1. Create and initialize a new project:

        ```bash
        mkdir papi-query-example && cd papi-query-example && \
        npm init -y && npm pkg set type=module
        ```

    2. Install dependencies:

        ```bash
        npm install polkadot-api && \
        npm install --save-dev @types/node tsx typescript
        ```

    3. Generate types for Polkadot Hub:

        ```bash
        npx papi add pah -n polkadot_asset_hub
        ```

    **Query Account Balance**

    The following example queries the `System.Account` storage to retrieve an account's native token balance.

    Create a file named `query-balance.ts` and add the following code to it:

    ```typescript title="query-balance.ts"
    --8<-- "code/chain-interactions/query-data/query-sdks/papi/query-balance.ts"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    npx tsx query-balance.ts
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/papi/query-balance-ts.html'

    **Query Asset Information**

    The following example queries the `Assets` pallet to retrieve metadata and balance information for USDT (asset ID 1984).

    Create a file named `query-asset.ts` and add the following code to it:

    ```typescript title="query-asset.ts"
    --8<-- "code/chain-interactions/query-data/query-sdks/papi/query-asset.ts"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    npx tsx query-asset.ts
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/papi/query-asset-ts.html'

=== "Polkadot.js"

    !!! warning "Maintenance Mode Only"
        The Polkadot.js API is no longer actively developed. New projects should use [PAPI](/reference/tools/papi/){target=\_blank} or [Dedot](/reference/tools/dedot/){target=\_blank} as actively maintained alternatives.

    **Prerequisites**

    - [Node.js](https://nodejs.org/){target=\_blank} v18 or higher
    - npm, pnpm, or yarn package manager

    **Environment Setup**

    1. Create and initialize a new project:

        ```bash
        mkdir pjs-query-example && cd pjs-query-example && \
        npm init -y && npm pkg set type=module
        ```

    2. Install dependencies:

        ```bash
        npm install @polkadot/api
        ```

    **Query Account Balance**

    The following example queries the `System.Account` storage to retrieve an account's native token balance.

    Create a file named `query-balance.js` and add the following code to it:

    ```javascript title="query-balance.js"
    --8<-- "code/chain-interactions/query-data/query-sdks/pjs/query-balance.js"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    node query-balance.js
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/pjs/query-balance-js.html'

    **Query Asset Information**

    The following example queries the `Assets` pallet to retrieve metadata and balance information for USDT (asset ID 1984).

    Create a file named `query-asset.js` and add the following code to it:

    ```javascript title="query-asset.js"
    --8<-- "code/chain-interactions/query-data/query-sdks/pjs/query-asset.js"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.
    
    Run the script:

    ```bash
    node query-asset.js
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/pjs/query-asset-js.html'

=== "Dedot"

    **Prerequisites**

    - [Node.js](https://nodejs.org/){target=\_blank} v18 or higher
    - npm, pnpm, or yarn package manager

    **Environment Setup**

    1. Create and initialize a new project:

        ```bash
        mkdir dedot-query-example && cd dedot-query-example && \
        npm init -y && npm pkg set type=module
        ```

    2. Install dependencies:

        ```bash
        npm install dedot && \
        npm install --save-dev @dedot/chaintypes @types/node tsx typescript
        ```

    **Query Account Balance**

    The following example queries the `System.Account` storage to retrieve an account's native token balance.

    Create a file named `query-balance.ts` and add the following code to it:

    ```typescript title="query-balance.ts"
    --8<-- "code/chain-interactions/query-data/query-sdks/dedot/query-balance.ts"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    npx tsx query-balance.ts
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/dedot/query-balance-ts.html'

    **Query Asset Information**

    The following example queries the `Assets` pallet to retrieve metadata and balance information for USDT (asset ID 1984).

    Create a file named `query-asset.ts` and add the following code to it:

    ```typescript title="query-asset.ts"
    --8<-- "code/chain-interactions/query-data/query-sdks/dedot/query-asset.ts"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    npx tsx query-asset.ts
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/dedot/query-asset-ts.html'

=== "Py Substrate Interface"

    **Prerequisites**

    - [Python](https://www.python.org/){target=\_blank} 3.8 or higher
    - pip package manager

    **Environment Setup**

    1. Create a new project directory and set up a virtual environment:

        ```bash
        mkdir psi-query-example && cd psi-query-example && \
        python3 -m venv venv && source venv/bin/activate
        ```

    2. Install the substrate-interface package:

        ```bash
        pip install substrate-interface
        ```

    **Query Account Balance**

    The following example queries the `System.Account` storage to retrieve an account's native token balance.

    Create a file named `query_balance.py` and add the following code to it:

    ```python title="query_balance.py"
    --8<-- "code/chain-interactions/query-data/query-sdks/psi/query_balance.py"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    python query_balance.py
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/psi/query-balance-py.html'

    **Query Asset Information**

    The following example queries the `Assets` pallet to retrieve metadata and balance information for USDT (asset ID 1984).

    Create a file named `query_asset.py` and add the following code to it:

    ```python title="query_asset.py"
    --8<-- "code/chain-interactions/query-data/query-sdks/psi/query_asset.py"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    python query_asset.py
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/psi/query-asset-py.html'

=== "Subxt"

    [Subxt](/reference/tools/subxt/){target=\_blank} is a Rust library that provides compile-time type safety through code generation from chain metadata.

    **Prerequisites**

    - [Rust](https://rustup.rs/){target=\_blank} toolchain (latest stable)
    - Cargo package manager

    **Environment Setup**

    1. Create a new Rust project:

        ```bash
        cargo new subxt-query-example && cd subxt-query-example
        ```

    2. Install the Subxt CLI:

        ```bash
        cargo install subxt-cli@{{ dependencies.crates.subxt_cli.version }}
        ```

    3. Download the Polkadot Hub metadata:

        ```bash
        subxt metadata --url INSERT_WS_ENDPOINT -o asset_hub_metadata.scale
        ```

        !!! note
            Ensure to replace `INSERT_WS_ENDPOINT` with the proper WebSocket endpoint, such as `wss://polkadot-asset-hub-rpc.polkadot.io` for Polkadot Hub.

    4. Update `Cargo.toml` with the required dependencies:

        ```toml title="Cargo.toml"
        --8<-- "code/chain-interactions/query-data/query-sdks/subxt/Cargo.toml"
        ```

    **Query Account Balance**

    The following example queries the `System.Account` storage to retrieve an account's native token balance.

    Create a file at `src/bin/query_balance.rs` and add the following code to it:

    ```rust title="src/bin/query_balance.rs"
    --8<-- "code/chain-interactions/query-data/query-sdks/subxt/src/bin/query_balance.rs"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    cargo run --bin query_balance
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/subxt/query-balance-rs.html'

    !!! note
        Subxt's `fetch()` method returns `None` for accounts with zero balance that have no on-chain storage entry, resulting in "Account not found". Accounts with activity will display their balance information.

    **Query Asset Information**

    The following example queries the `Assets` pallet to retrieve metadata and balance information for USDT (asset ID 1984).

    Create a file at `src/bin/query_asset.rs` and add the following code to it:

    ```rust title="src/bin/query_asset.rs"
    --8<-- "code/chain-interactions/query-data/query-sdks/subxt/src/bin/query_asset.rs"
    ```

    !!! note
        Ensure to replace `INSERT_WS_ENDPOINT` with a valid WebSocket endpoint (e.g., `wss://polkadot-asset-hub-rpc.polkadot.io`) and `INSERT_ADDRESS` with the account address you want to query.

    Run the script:

    ```bash
    cargo run --bin query_asset
    ```

    You should see output similar to:

    --8<-- 'code/chain-interactions/query-data/query-sdks/subxt/query-asset-rs.html'

