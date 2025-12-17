# Deploy to Cloud (AWS)

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 1.47.17 PM.png>)

**Typical Platform Deployment Time : 10 \~15 minutes**

Deploy the platform to AWS using our provided script. The script simplifies the process and provides the platform URL upon completion. With this, your platform will be hosted on the cloud and accessible from anywhere in the world.

#### Security Credentials

* AWS Access key - Obtain your AWS access and secret keys from the AWS IAM console. Log in to your AWS account and follow the official [AWS documentation](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html) to generate these keys.

#### Software Prerequisites

If any of the packages listed below are missing on your machine, you can use our automated script to install them.

* [Git](https://git-scm.com/)
* [Make](https://www.gnu.org/software/make/)
* [Terraform](https://developer.hashicorp.com/terraform)
* [AWS CLI](https://aws.amazon.com/cli/)



1.  On your local machine, open a terminal and download the dependencies

    ```bash
    curl -L -O https://raw.githubusercontent.com/tokamak-network/trh-platform/main/install.sh

    ```
2.  Change permission of the dependency script

    ```bash
    chmod +x install.sh
    ```
3.  Install the dependencies

    ```bash
    ./install.sh 
    ```
4. After successful installation, you will see the below message.

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 1.47.58 PM.png>)

#### Deploy Tokamak Rollup Hub Platform

1.  On your local machine, open a terminal and clone the TRH-Platform repository.<br>

    ```bash
    # clone the trh-platform repository
    git clone https://github.com/tokamak-network/trh-platform
    # change directory to trh-platform
    cd trh-platform

    ```
2.  Run the below command in your terminal for the configuration.<br>

    ```bash
    # setup for ec2 deployment
    make ec2-setup
    ```

    \
    You will be asked to put the following parameters. You can use default values for some of them.&#x20;

    * Key credentials: AWS access key & AWS secret access key (If you don’t have any AWS access key, please refer [this guide](https://repost.aws/knowledge-center/create-access-key) and create new one.)
    * AWS region (default: ap-northeast-2): The region where the ec2 instance for platform is installed
    * SSH key pai&#x72;**:** _The key pair name for SSH access. Please keep this noted so you can use it when you try to access EC2 instance via SSH. The key is generated to `~/.ssh`_

    \
    Note: Terraform will automatically generate and store a new key pair on AWS and your machine (`~/.ssh`). Do not create this manually - just provide a name (e.g., "my-ec2-key").<br>
3.  Run the below command in your terminal. This will launch an EC2 instance and deploy the platform on it. After deployment, a success message will appear along with the platform URL for access.<br>

    ```bash
    # deploy ec2
    make ec2-deploy
    ```



    * Instance Type (default: t2.large): _The T-shirt size of EC2 instance_
    * Instance Nam&#x65;**:** _The name of your EC2 instance_

    Platform Auth configuration (The below credentials will help you to login to the platform)

    * Admin Email (default: _**admin@gmail.com**_): The email which will be used for platform login
    * Admin Password (default: _**admin**_)**:** The password which will be used for platform login

    \
    After deployment, you will receive the instance hostname as shown in the below screenshot, along with the platform dashboard URL. \
    <br>

    ![](<../../../../.gitbook/assets/Deployed Logs.png>)
4.  Get AWS EC2 information<br>

    ```bash
    make ec2-status
    ```
5.  Destroy AWS EC2 instance

    \
    Note : Terminating the EC2 instance will not remove any deployed chains. Chains must be deleted directly from the platform. Destroying the EC2 instance only removes the instance itself along with the platform running on it.<br>

    ```bash
    make ec2-destroy
    ```

