---
description: Choose the deployment style, install and prepare the SDK for use.
---

# Getting Started

This section guides you through selecting a deployment style, followed by SDK setup.

{% hint style="warning" %}
**Note:** For both **Testnet** and **Mainnet** deployments, the appchain infrastructure is deployed on **AWS**. Prerequisites and setup details for AWS are provided in the respective deployment sections. Support for additional cloud providers will be introduced in future releases.
{% endhint %}

### Hardware requirements & Software Requirements

Please verify that your system meets these hardware requirements prior to starting the SDK setup.

|             | CPU    | RAM | Storage |
| ----------- | ------ | --- | ------- |
| Minimum     | 2 vCPU | 4   | 20      |
| Recommended | 4 vCPU | 8   | 50      |

{% hint style="info" %}
Users must have an AWS account to proceed with Testnet or Mainnet deployment.
{% endhint %}

### Deployment Style

We offer **three flexible deployment styles** to support a range of developer environments. Choose the one that best fits your needs:

***

**1. Local Machine Deployment (macOS and Linux)**

In this approach, the SDK is installed and run directly on your **local machine** to deploy an appchain.

* Supports both **Devnet** and **Testnet** deployments. (Note : Testnet infra will be deployed in AWS)
* To use this method, follow the **SDK setup instructions** in your local machine.

***

**2. EC2-Based Deployment (Preferred Choice)**

This method allows you to deploy the appchain from an **AWS EC2 instance**.

* Begin by launching and configuring an EC2 instance using this [step-by-step guide](https://www.notion.so/A-Step-by-Step-Guide-to-Launching-Operating-an-EC2-Instance-on-AWS-1d0d96a400a3805a94a4f92c31d964c9?pvs=21).
* Once your EC2 instance is ready and accessible, continue with the SDK setup and deployment process.

***

**3. Docker-Based Deployment**

This approach uses a **Docker container** to deploy the chain.

* Currently supports **Testnet** deployments only.
* Useful for isolated or containerized environments.
* To get started, follow this [Docker setup guide](https://www.notion.so/User-guide-for-TRH-SDK-Docker-image-1d6d96a400a380dc8481ea308eadda93?pvs=21).
* Once your Docker environment is ready, proceed with the SDK setup and deployment steps.

### SDK Setup

Follow these step-by-step instructions to set up the SDK:

1.  Download the [setup.sh](https://github.com/tokamak-network/trh-sdk/blob/main/setup.sh) file

    ```bash
    curl https://raw.githubusercontent.com/tokamak-network/trh-sdk/main/setup.sh > setup.sh
    ```
2.  Run the [setup.sh](https://github.com/tokamak-network/trh-sdk/blob/main/setup.sh) file

    ```bash
    chmod +x setup.sh
    ./setup.sh
    ```
3.  Source the shell config

    MacOS

    ```bash
    source ~/.zshrc
    ```

    Linux

    ```bash
    source ~/.bashrc
    ```
4.  Verify the installation

    ```bash
    trh-sdk version

    ## The expected output of this command
    v0.0.0-${commit-id}
    ```



This completes the SDKv1 setup on your instance. You can now proceed to the Rollup Stack section to explore the available stacks and their respective deployment options.
