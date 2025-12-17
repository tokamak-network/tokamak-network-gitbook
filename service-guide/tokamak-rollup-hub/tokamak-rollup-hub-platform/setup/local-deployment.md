# Local Deployment

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 12.50.37 PM.png>)

## Sections :

1. Hardware requirement
2. Platform setup steps
3. How to access the platform?
4. How to stop the platform?
5. Platform logs

In this setup, you can run the platform directly on your local machine. Please follow the below steps to complete your setup.

**Note**: We have tested the platform setup on Linux and Mac machines. If you encounter any issues during setup, please contact the Tokamak Rollup Hub team via [discord](https://discord.com/channels/696270789472682034/1239385660893167616).

### Hardware Requirement

<table data-full-width="true"><thead><tr><th></th><th>CPU</th><th>RAM</th><th>Storage</th></tr></thead><tbody><tr><td>Minimum</td><td>2 vCPU</td><td>8</td><td>30</td></tr><tr><td>Recommended</td><td>4 vCPU</td><td>16</td><td>50</td></tr><tr><td>Excellent</td><td>8 vCPU</td><td>32</td><td>70</td></tr></tbody></table>

### Platform Setup

#### 1. Clone the repository

Open your terminal and execute the below command

```bash
git clone https://github.com/tokamak-network/trh-platform
cd trh-platform
```

#### 2. Setup script and installing dependencies

&#x20; a.  Change permission of the dependency script.

```bash
chmod +x install.sh
```

&#x20; b.  Install the dependencies.

```bash
./install.sh 
```

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 12.52.41 PM.png>)

&#x20;c.  Setup _config_ files.

```
make config
```

You will then be prompted with questions in the terminal. Press Enter to use the default values or provide your own inputs.

```bash
`api base url use - [http://localhost:8000](http://localhost:8000/)`

`Admin Configuration -`

`email - [admin@gmail.com](mailto:admin@gmail.com)`

`password - admin`
```

Once you’ve entered all the required inputs, press Enter to complete the environment variables setup. Please refer to below screenshot.&#x20;

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 12.58.41 PM.png>)

d.  Run the following command in your terminal to start your platform.

```bash
make setup
```

You should expect to see the following logs when you run the above command in the terminal.

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 12.07.19 PM.png>)

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 12.08.42 PM.png>)

#### 3. How to access the platform?

&#x20; a.  After the successful installation, you can access the platform by navigating to [http://localhost:3000/](http://localhost:3000/**) in your browser.

&#x20; b.  Log in using the email ID and password you set during the config file setup in previous step.

![](<../../../../.gitbook/assets/Screenshot 2025-12-05 at 1.02.32 PM.png>)

#### 4. How to stop the platform?

Run the following command to stop your platform. It won’t delete any deployed chain, and your chain will remain available when you restart the platform.

```bash
make down
```

You will see the following logs when you run the above command.

![](<../../../../.gitbook/assets/Screenshot 2025-12-03 at 1.29.31 PM.png>)

#### **5.** How to check the platform logs?

Run the following command to check the logs.

```bash
make logs
```
