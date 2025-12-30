## Alerting

### Why Are We Moving Away from Classic Alerting?
Dynatrace Classic alerting relied on:
- **Problem Notifications**: Defined where notifications were sent (channels, integrations).
- **Alerting Profiles**: Defined what problems triggered notifications using reusable filters.

However, there are certain limitations of Classic Alerting:
- **Rigid integrations**: Hardcoded, lacked flexibility.
- **Only for problems**: Couldn’t trigger on specific events.
- **Confusing notifications**: Limited context.
- **No execution transparency**: No way to inspect delivery status or debug failures.


### Why Davis Anomaly Detection?
Dynatrace Gen3 introduces Davis Anomaly Detection powered by Grail:
- **Dynamic, AI-driven detection**: Automatically adapts to metric behavior.
- **Improved accuracy**: Reduces false positives and manual threshold tuning.
- **Event-driven automation**: Works with Workflows for intelligent responses.
- **Transparency**: Full visibility into execution logs and outcomes.


### Why Workflows?
Move beyond static alerting to **dynamic, customizable automation.**
Define **how, when, and where** actions should happen.
Trigger notifications, remediation scripts, ticket creation, and more.
Works for **any event stored in Grail** (problems, Davis events, generic events).
Provides **execution transparency** for troubleshooting and validation.


### Lab Objectives
By the end of this lab, you will:
1. Transform an existing metric event into a Davis anomaly detector.
2. Validate the anomaly detection configuration.
3. Create a workflow that reacts to a dt.davis.problem event and sends an email notification.


### Hands-On Steps

#### Step 1: Review Existing Metric Event

- Navigate to Settings → Anomaly Detection → Metric Events.
- Locate the pre-existing metric event → "Test Alert - Metric Selector - Static Threshold" .

![](../../assets/images/metricevent.png)


#### Step 2: Transform Metric Event to Davis Anomaly Detector

- Go to Anomaly Detection → Davis Anomaly Detection. 
- Click + New Alert.
![](../../assets/images/metricevent.png)
- Choose "Improve metric events with DQL".
![](../../assets/images/improvewithdql.png)
- Select the existing metric event "Test Alert - Metric Selector - Static Threshold" and click "Transform".
![](../../assets/images/transformmetricevent.png)
![](../../assets/images/davisanomalydetection.png)
- Review the transformation screen showing metric event → anomaly detector - DQL editor with generated query.
![](../../assets/images/anomalydetectordql.png)
- Review the generated DQL query and adjust if needed.

#### Step 3: Validate Anomaly Detection

- Trigger a test scenario or wait for real data.
- Confirm that Davis detects anomalies as expected.
![](../../assets/images/problemcard.png)
![](../../assets/images/problemcarddetails.png)

#### Step 4: Create a Workflow for Email Notification

- Navigate to Workflows → + Create Workflow.
- Select Trigger: Davis Problem Event (dt.davis.problem).
- Add an Action: Send Email.

Configure recipient email (provided in lab instructions).
Add subject and body placeholders (e.g., problem details).

Save and activate the workflow.

Screenshot Placeholder:

Workflow builder showing trigger and email action.
Email configuration panel.


#### Step 5: Test the Workflow

- Simulate a Davis problem or use an existing anomaly.
- Verify that the email notification is sent successfully.
- Check workflow execution logs for transparency.
- Screenshot Placeholder: Workflow execution log and email received.


Key takeaway: Alerting in Gen3 is not just about notifications—it’s about intelligent, event-driven automation that adapts to your environment.

We hope you thoroughly enjoyed all of our labs! 

Time for Q&A!