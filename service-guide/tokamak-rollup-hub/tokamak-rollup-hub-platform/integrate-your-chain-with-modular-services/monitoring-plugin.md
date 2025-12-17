# Monitoring Plugin

1. **Pre-requisites:** Before installing the monitoring plugin, review the [notion guide](https://tokamak.notion.site/Tokamak-Rollup-Hub-Platform-Monitoring-plugin-Guide-2cad96a400a3803ea1e4c4225d49af43) and prepare the required details. To receive updates through Gmail, you must configure a Telegram bot and create App password.
2. Once the prerequisites are met, navigate to the Integrations tab of the deployed chain and select _Install Monitoring Plugin_.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.23.06 PM.png" alt=""><figcaption></figcaption></figure>

3. Input a password for the grafana dashboard

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-03 at 5.21.17 PM.png" alt=""><figcaption></figcaption></figure>

4. To receive criteria alerts via Telegram or Email, please fill the appropriate fields using the prerequisite details that you have prepared. (All fields are mandatory)
   * Telegram Alerts
     * Telegram Bot API token: API Token for your personal bot. This token allows bots to send messages or process user requests.
     * Chat IDs: Unique ID for identifying a particular conversation. It is required when the bot automatically sends a message to a particular chat room.
   * Email Alerts
     * SMTP Server: Now it is fixed to [smtp.gmail.com:587](http://smtp.gmail.com:587)
     * From Email: Sender address
     * SMTP Password: App-only password for sending mail via [smtp.gmail.com](http://smtp.gmail.com)
     * Alert Receivers: Receiver addresses (at least one)

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-03 at 5.22.14 PM.png" alt=""><figcaption></figcaption></figure>

5. Next, open the Deployment History tab to track the initiation of the deployment and verify its completion.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.22.10 PM.png" alt=""><figcaption></figcaption></figure>

6. Review the logs and dashboard to confirm that the installation was successful.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.18.27 PM.png" alt=""><figcaption></figcaption></figure>

7. You can check the integrations tab and find the status of the component which is installed.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.23.56 PM.png" alt=""><figcaption></figcaption></figure>

8. Now you can find the Grafana Dashboard button on Quick Links to access your monitoring dashboard. (Default username is admin) You can refer this [guide](https://tokamak.notion.site/Tokamak-Rollup-Hub-Platform-Monitoring-plugin-Guide-2cad96a400a3803ea1e4c4225d49af43) for operating monitoring plugin.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.25.25 PM.png" alt=""><figcaption></figcaption></figure>
