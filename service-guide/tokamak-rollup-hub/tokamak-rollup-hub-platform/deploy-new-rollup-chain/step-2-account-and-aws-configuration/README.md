# Step 2 - Account and AWS Configuration

1. In this step, the user will be prompted to enter the seed phrase for the account holding the Ether balance (Testnet) needed to deploy the chain. If you want to know more about this, please see [this](https://docs.tokamak.network/home/~/revisions/2GhxIXb1VQ8ZXausKkQz/service-guide/tokamak-rollup-hub/tokamak-rollup-hub-platform/deploy-new-rollup-chain/step-3-account-and-aws-configuration/seed-phrase-guidelines) section.&#x20;
2.  If the user does not provide a seed phrase, the platform can automatically generate one. This can be done by clicking the Generate Random button. After generating the seed phrase, make sure to fund the associated address with the required Sepolia ETH. Please refer to this [section](https://docs.tokamak.network/home/~/revisions/2GhxIXb1VQ8ZXausKkQz/service-guide/tokamak-rollup-hub/tokamak-rollup-hub-platform/deploy-new-rollup-chain/step-3-account-and-aws-configuration/seed-phrase-guidelines) for more details about the required ETH balance.<br>

    ![](<../../../../../.gitbook/assets/Screenshot 2025-12-05 at 2.54.17 PM.png>)
3. To deploy successfully, the operator must configure AWS credentials with specific privileges to access Amazon EKS. Follow the stages below to prepare your environment.\
   \
   **Phase 1: IAM User & Credential Setup**\
   If you do not have an existing AWS Access Key, you must create an IAM user and generate new keys.\
   To create an IAM User, Follow steps 1 to 9 in the [IAM Creation Guide](https://docs.tokamak.network/home/~/changes/151/service-guide/tokamak-rollup-hub/tokamak-rollup-hub-deprecated/mainnet-beta/deploy-with-aws/prerequisites#id-4.-set-up-aws-account).&#x20;

> What is IAM? AWS Identity and Access Management (IAM) enables you to manage access to AWS services and resources securely. You can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

&#x20;      **Phase 2: Operator Deployment**\
&#x20;      Once the IAM user and keys are ready, proceed to the deployment selection screen as \
&#x20;      shown below.\
&#x20;      The operator must select an AWS key to authorize the deployment:\
&#x20;         \-  Existing Users: Choose a saved key from the list.\
&#x20;         \-  New Users: Select "Add New" and input the Access Key and Secret Key generated in\
&#x20;             phase 1.&#x20;

![](<../../../../../.gitbook/assets/Screenshot 2025-12-05 at 2.54.59 PM.png>)

![](<../../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.30.06 PM.png>)

4. Once the key is selected, please choose a region for the deployment<br>

![](<../../../../../.gitbook/assets/Screenshot 2025-12-05 at 2.55.28 PM.png>)

5. Click Next in the platform.
