---
description: >-
  Launch and connect to an AWS EC2 instance to run the TRH SDK — the recommended
  environment for Testnet and Mainnet deployments.
---

# EC2-Based Deployment

The **EC2-based** deployment style runs the TRH SDK from an **AWS EC2 instance** instead of your local machine. This is the recommended environment for Testnet and Mainnet deployments.

{% hint style="info" %}
**Why run the SDK from EC2?**

* A deployment takes roughly 40–50 minutes and the SDK keeps orchestrating AWS infrastructure throughout — an always-on instance won't be interrupted by your laptop sleeping or losing network.
* After deployment, the operator processes keep running on the instance.
* The instance sits close to the AWS resources the SDK manages, and gives a clean, consistent Linux environment that matches the prerequisites.
{% endhint %}

## Prerequisites

* An **AWS account** with permission to create EC2 instances.
* An SSH client (built into macOS/Linux; on Windows use PowerShell, WSL, or PuTTY).

## 1. Choose an instance size

Pick an instance type and disk that meet the SDK's requirements:

|             | vCPU | RAM (GB) | Storage (GB) | Example instance type |
| ----------- | ---- | -------- | ------------ | --------------------- |
| Minimum     | 2    | 4        | 20           | `t3.medium`           |
| Recommended | 4    | 8        | 50           | `t3.xlarge`           |

{% hint style="info" %}
Use a 64-bit (x86\_64 / amd64) Linux AMI such as a recent **Ubuntu LTS**. Use `gp3` EBS storage sized at or above the recommended value.
{% endhint %}

## 2. Launch the EC2 instance

From the AWS Console → **EC2** → **Launch an instance**:

1. **Name** — give the instance a recognizable name (e.g., `trh-sdk`).
2. **AMI** — select a recent **Ubuntu LTS** image.
3. **Instance type** — choose a type that meets the requirements above (e.g., `t3.xlarge`).
4. **Key pair** — create or select an SSH key pair, and download the private key (`.pem`) if creating a new one. You'll need it to connect.
5. **Network / security group** — allow **inbound SSH (TCP port 22)** from **your IP address only**.
6. **Storage** — set the root volume to at least the recommended size (e.g., 50 GB `gp3`).
7. Click **Launch instance**.

## 3. Connect to the instance

Once the instance is **Running**, copy its **Public IPv4 address** (or Public DNS) and connect over SSH. For an Ubuntu AMI the default user is `ubuntu`:

```bash
chmod 400 /path/to/your-key.pem
ssh -i /path/to/your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

{% hint style="warning" %}
Keep your `.pem` private key safe and restrict the SSH security-group rule to your own IP. Anyone with the key and an open port can access the instance.
{% endhint %}

## 4. Continue with the SDK setup

Once you are connected to the instance, follow the **SDK Setup** steps on the [Getting Started](getting-started.md) page to install `trh-sdk`, then proceed with your deployment.

***

For the full set of EC2 options (regions, IAM roles, Elastic IPs, etc.), see the official AWS documentation: [Get started with Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html).
