# System Pulse

System Pulse provides real-time visibility into platform health and service availability. It can also be installed or uninstalled as required.

1. To install the system pulse service navigate to the Integrations tab of the deployed chain and select Install System Pulse.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.27.00 PM.png" alt=""><figcaption></figcaption></figure>

2. Open the Deployment History tab to track the initiation of the deployment and verify its completion.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-05 at 3.27.41 PM.png" alt=""><figcaption></figcaption></figure>

3. You can check the integrations tab and find the status of the component which is installed.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-03 at 5.29.55 PM.png" alt=""><figcaption></figcaption></figure>

4. Now you can find the System Pulse button on Quick Links to access your monitoring dashboard.

***

## Operating System Pulse

### 1. Set Up Admin Credentials

On first access, the service redirects you to a setup page before showing the dashboard.

1. Navigate to your System Pulse dashboard URL (accessible via the Quick Links button).
2. You will be prompted to create the primary administrator account.
3. Enter a secure **Username** and a strong **Password**.
4. Confirm the password and complete the setup.

This account has full administrative rights to add monitors, configure status pages, and manage system settings.

***

### 2. List All Services to Monitor

Before configuration, identify all critical endpoints and services that require uptime monitoring. For each service, gather:

- **Monitor Type:** The protocol to use (e.g., `HTTP(s)`, `Ping`).
- **Service URL / IP:** The specific endpoint, IP address, or domain to target.
- **Success Criteria:** For HTTP monitors, the expected "Up" status code (e.g., `200`).

***

### 3. Add a Monitor for Each Service

1. From the main dashboard, click **"+ Add New Monitor"**.
2. **Select Monitor Type:** Choose the correct type (e.g., `HTTP(s)`).
3. **Friendly Name:** Enter a human-readable name for the service.
4. **URL:** Enter the service URL to be monitored.
5. **Heartbeat Interval:** Set the check frequency (e.g., `20 seconds`).
6. **Notifications:** Configure alerting integrations (e.g., Slack, Telegram) to be notified on a "Down" event.
7. Click **"Save"**.
8. Repeat for all services on your list.

***

### 4. Create a Status Page

1. In the top navigation bar, click **"Status Pages"**.
2. Click **"+ Add New Status Page"**.
3. **Page Name:** Enter a title (e.g., `TRH Platform Status`).
4. **Slug / URL:** Define the custom URL path (e.g., enter `trh` to publish at `/status/trh`).
5. **Theme & Customization:** Optionally add a company logo, custom CSS, or a site description.
6. Click **"Next"** to proceed to service configuration.

***

### 5. Create Groups and Assign Monitors

Organize services into logical categories on the status page.

1. While editing the new status page, click **"+ Add Group"**.
2. **Group Name:** Enter a logical category name (e.g., `Core Infrastructure`, `L2 Services`, `APIs & Endpoints`).
3. Click **"Save"**.
4. Drag and drop the monitors created in Step 3 into the appropriate groups.

The published status page will display live service health organized by group, accessible at the slug path you defined (e.g., `/status/trh`).

***

#### Uninstallation

The operator can uninstall the System Pulse by clicking the bin icon and confirming the action.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-08 at 4.24.05 PM.png" alt=""><figcaption></figcaption></figure>
