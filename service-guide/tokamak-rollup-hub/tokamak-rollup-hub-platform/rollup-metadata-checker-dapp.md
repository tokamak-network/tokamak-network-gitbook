# Rollup Metadata Checker DApp

<figure><img src="../../../.gitbook/assets/Screenshot 2025-12-03 at 4.48.16 PM.png" alt=""><figcaption></figcaption></figure>

Rollup Metadata Checker is a tool to verify the validity of L2 rollup information registered in [the Tokamak Rollup Metadata Repository](https://github.com/tokamak-network/tokamak-rollup-metadata-repository/tree/main/data). It allows users to check not only the L1/L2 information of the rollup they want to inspect, but also verifies whether the L1/L2 contracts are identical to the official deployment version.

### Prerequisites

To check and verify validity of an L2 rollup, The chain needs to be up and running with metadata registered through either the platform or the sdk and the PR must be merged in the [metadata repo](https://github.com/tokamak-network/tokamak-rollup-metadata-repository).

Check the following to register metadata - [Register Metadata](https://docs.tokamak.network/home/service-guide/tokamak-rollup-hub/tokamak-rollup-hub-platform/register-metadata)

#### Step 1

Clone the rollup metadata checker application

```
git clone https://github.com/tokamak-network/tokamak-rollup-metadata-checker.git
```

#### Step 2

Checkout the example-app directory, install dependencies and run the application

```
cd example-app

npm i

npm run dev
```

#### Step 3

Open the ui on - `http://localhost:3000`

To check the metadata L1 and L2 verification for a chain, user could check:

`http://localhost:3000/rollup/`
