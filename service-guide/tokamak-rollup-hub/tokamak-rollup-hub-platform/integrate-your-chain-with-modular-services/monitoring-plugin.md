# Monitoring Plugin

1. **Pre-requisites:** Before installing the monitoring plugin, ensure your L2 chain is running on the Tokamak Rollup Hub Platform. If you want to receive alerts, prepare the following credentials in advance — you will need them during installation.

   **Telegram Alert Setup**

   Store the API Token and Chat ID from the steps below; they are required during plugin installation.

   * Create a Telegram bot
     * Open Telegram and search for **@BotFather** or visit [https://t.me/botfather](https://t.me/botfather)
     * Run `/newbot`, enter a bot name (e.g. "Monitoring Alert Bot") and a username (e.g. "my\_monitoring\_bot")
   * Get your API Token
     * Run `/mybots` in BotFather and select the bot you created
     * Select **API Token** — BotFather returns a token in the format `1234567890:ABCdefGHIjklMNOpqrsTUVwxyz`. Store it securely.
   * Get your Chat ID
     * Start a conversation with your bot by sending `/start`
     * Open the following URL in a browser (replace `<YOUR_BOT_TOKEN>` with your token): `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
     * The response JSON contains a `chat.id` field — that is your Chat ID

   **Email Alert Setup** (Gmail only)

   Store the App Password from the steps below; it is required during plugin installation.

   * Visit [https://myaccount.google.com/security](https://myaccount.google.com/security) and enable **2-Step Verification**
   * After enabling 2-Step Verification, navigate to **2-Step Verification → App passwords**
   * Enter a name (e.g. "Monitoring Alert") and copy the generated 16-character password

2. Once the prerequisites are met, navigate to the Integrations tab of the deployed chain and select _Install Monitoring Plugin_.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.23.06 PM.png" alt=""><figcaption></figcaption></figure>

3. Input a password for the grafana dashboard

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-03 at 5.21.17 PM.png" alt=""><figcaption></figcaption></figure>

4. To receive criteria alerts via Telegram or Email, please fill the appropriate fields using the prerequisite details that you have prepared. (All fields are mandatory)
   * Telegram Alerts
     * Telegram Bot API token: API Token for your personal bot. This token allows bots to send messages or process user requests.
     * Chat IDs: Unique ID for identifying a particular conversation. It is required when the bot automatically sends a message to a particular chat room.
   * Email Alerts
     * SMTP Server: Now it is fixed to [smtp.gmail.com:587](http://smtp.gmail.com:587)
     * From Email: Sender address
     * SMTP Password: App-only password for sending mail via [smtp.gmail.com](http://smtp.gmail.com)
     * Alert Receivers: Receiver addresses (at least one)

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-03 at 5.22.14 PM.png" alt=""><figcaption></figcaption></figure>

5. Next, open the Deployment History tab to track the initiation of the deployment and verify its completion.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.22.10 PM.png" alt=""><figcaption></figcaption></figure>

6. Review the logs and dashboard to confirm that the installation was successful.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.18.27 PM.png" alt=""><figcaption></figcaption></figure>

7. You can check the integrations tab and find the status of the component which is installed.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.23.56 PM.png" alt=""><figcaption></figcaption></figure>

8. Now you can find the Grafana Dashboard button on Quick Links to access your monitoring dashboard. The default username is `admin` and the password is what you set during installation.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.25.25 PM.png" alt=""><figcaption></figcaption></figure>

## Operating the Monitoring Dashboard

### Accessing Dashboards

Navigate to **Home → Dashboards** in Grafana. The following dashboards are available:

* Thanos Stack Application Monitoring Dashboard
* Thanos Stack Blackbox Monitoring Dashboard
* Thanos Stack System Resource Monitoring Dashboard

### Checking Alert Rules

Navigate to **Home → Alerting → Alert rules** to view the real-time status, trigger conditions, and evaluation queries for the 11 default alert rules.

| Category | Alert Rules | Response Time | Description |
| --- | --- | --- | --- |
| **Service Health** | `OpNodeDown`, `OpBatcherDown`, `OpProposerDown`, `OpGethDown` | 45 seconds | Thanos Stack service availability monitoring |
| **Network** | `L1RpcDown` | 25 seconds | L1 RPC connection status |
| **Financial** | `OpBatcherBalanceCritical`, `OpProposerBalanceCritical` | 25 seconds | ETH balance monitoring (less than 0.01 ETH) |
| **Blockchain** | `BlockProductionStalled` | 1 min 15 sec | Block production stopped for 1m |
| **Resources** | `ContainerCpuUsageHigh`, `ContainerMemoryUsageHigh` | 2 min 15 sec | Resource usage above 80% |
| **Stability** | `PodCrashLooping` | 2 min 15 sec | Pod restart loop detection during 2 minutes |

{% hint style="info" %}
Sensitive information such as API tokens and passwords is never displayed in plain text in the Grafana UI.
{% endhint %}

### Checking Alert Channels

Navigate to **Home → Alerting → Contact points** to see the alert channel settings configured during installation. Alert channel settings are read-only and managed directly in the pod.

### Querying Logs

Navigate to **Home → Explore**, change the data source to **CloudWatch**, and select your region. Log groups are automatically created for each component (`op-node`, `op-geth`, `op-batcher`, `op-proposer`) during installation.

Useful CloudWatch Insights queries:

```bash
# Retrieve up to the 200 most recent log entries
fields @timestamp, @message |
 sort @timestamp desc |
 limit 200

# Retrieve the 50 most recent log entries matching keywords
fields @timestamp, @message
| filter @message like /payload|chain|block|imported/
| sort @timestamp desc
| limit 50

# Retrieve log entries within a specific timestamp range (milliseconds)
fields @timestamp, @message
| filter @timestamp >= 1753787368000
| filter @timestamp <= 1754387368000
| limit 100
```

### Customizing Alerts

After installation, use the `trh-sdk alert-config` command to manage notification channels and adjust alert thresholds. Changes apply automatically without restarting Alertmanager.

```bash
# Check current alert status and active rules
trh-sdk alert-config --status

# Configure email channel
trh-sdk alert-config --channel email --configure

# Configure Telegram channel
trh-sdk alert-config --channel telegram --configure

# Disable a channel
trh-sdk alert-config --channel email --disable
trh-sdk alert-config --channel telegram --disable

# Adjust alert thresholds interactively (balance, CPU, memory, etc.)
trh-sdk alert-config --rule set

# Reset all alert rules to defaults
trh-sdk alert-config --rule reset
```

Six configurable alert rules can have their thresholds adjusted or be individually enabled/disabled: `OpBatcherBalanceCritical`, `OpProposerBalanceCritical`, `BlockProductionStalled`, `ContainerCpuUsageHigh`, `ContainerMemoryUsageHigh`, and `PodCrashLooping`. The five core service health rules (`OpNodeDown`, `OpBatcherDown`, `OpProposerDown`, `OpGethDown`, `L1RpcDown`) cannot be modified.

### Managing Log Collection

Use the `trh-sdk log-collection` command to enable/disable log collection, adjust retention and collection interval, or download logs.

```bash
# Enable log collection (default: 30-day retention, 30s interval)
trh-sdk log-collection --enable

# Set retention period to 90 days and interval to 60 seconds
trh-sdk log-collection --retention 90 --interval 60

# Show current logging configuration
trh-sdk log-collection --show

# Download logs for a specific component (last 7 hours)
trh-sdk log-collection --download --component op-node --hours 7

# Download logs for all components filtered by keyword (last 24 hours)
trh-sdk log-collection --download --component all --hours 24 --keyword error

# Disable log collection
trh-sdk log-collection --disable
```

## Troubleshooting

**Alerts not working**

```bash
# Check alert status
trh-sdk alert-config --status

# Reset alert rules to defaults
trh-sdk alert-config --rule reset

# Restart Prometheus/Alertmanager
kubectl rollout restart ${deployment/prometheus} -n monitoring
kubectl delete pod ${pod/alertmanager} -n monitoring

# Check Alertmanager logs
kubectl logs -n monitoring ${pod/alertmanager} --tail=20

# Inspect alert rules
kubectl get configmap ${rulefile/prometheus} -n monitoring -o yaml
```

**Email alerts not sending**

* Verify your App Password is correct (not your regular Google account password)
* Confirm SMTP settings: server is `smtp.gmail.com:587`, username matches the From address
* Check that no firewall or network policy is blocking outbound port 587

**Telegram alerts not sending**

* Verify the bot token is correct
* Confirm the Chat ID is correct
* Ensure the bot has permission to send messages to the target chat

**Dashboard not accessible**

```bash
# Check pod status
kubectl get pods -n monitoring

# Restart Grafana
kubectl rollout restart ${deployment/grafana} -n monitoring
```
