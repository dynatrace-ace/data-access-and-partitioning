## Dashboard Upgrade

The Eastrade team has been using their own classic dashboard for years, and they want to make sure to have it for 3rd Gen. They are also curious on how they can improve their dashboards with all the new functionalities.

Dynatrace allows you to track the classic dashboards popularity. This is a great feature when moving into 3rd Gen, to reduce the scope, and focus the upgrade in what matters. The Easytrade team has received a notification from the Dynatrace Admins in the organization, that the EasyTrade dashboard needs an upgrade. The teams agree with the statement, since it is the most used dashboard, and they proceed with the instructions.

![](../../assets/images/popularity.png)

### Automated!

1. Go to classic dashboards and open the easytrade dashboard, check how the dashboard has a predefined Management Zone filter 

![](../../assets/images/dashboard-classic.png)

2. Click on the 3-dots, then Upgrade. Notice that the existing classic dashboard will remain the same, it is not lost during the upgrade

![](../../assets/images/upgradebutton.png)

3. The previous dashboard was filtering by Management Zone. The new dashboard then needs to filter by Segment. As we already have a solid Segment definition, our dashboard should work as well

![](../../assets/images/configuresegmentdash.png)

### Manual leftovers

Some tiles are not automatically upgraded, [check official doc](https://docs.dynatrace.com/docs/analyze-explore-automate/dashboards-classic/dashboards-upgrade-classic-to-latest#in-scope-not-yet). 

4. Create a new DQL tile

![](../../assets/images/newdql.png)

5. Use this DQL code, and click run

```
fetch dt.davis.problems
| filter dt.davis.is_duplicate == false
| fields display_id, event.status
| summarize {Open = countIf(event.status != "CLOSED"), Closed = countIf(event.status == "CLOSED")}, by:{display_id}
```

![](../../assets/images/runproblemsdql.png)

#### Upgrade SLOs (Optional)

6. Go to classic SLOs and open the metric in metric explorer

7. In metric explorer open the advanced expression in notebooks

8. In the DQL statement, replace in the last line the field `expression` with sli

9. Copy the DQL statement and open the SLO app

10. In the SLO app add a new custom SLO

11. Pin the SLO to dashboard

#### Enhance

12. Improve dashboard with tiles & views that were not possible before. E.g. Exceptions? Logs? Business events?​. Pin top database queries on dashboard from services

![alt text](dashboard-enhanced.png)