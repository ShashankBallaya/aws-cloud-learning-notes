# Amazon CloudWatch - Monitoring and Obervability 

**Date Studied:** 06 April 2026
**Week:** 4 | **DAy:** 1 | **Status:** Conmplete

---

## What Is It?
CloudWatch monitors your AWS resources and applications so you can see performance, detect issues, and get alerted automatically.

## How It Works (Key Concepts)
- Metrics: Numerical data (CPU, memory, requests) collected over time.
- Dashboard: Visual display of multiple metrics in one place.
- Alarm: Triggers action when a metric crosses a treshold.
- SNS: Sends notifications (email, SMS) when alarms trigger.
- Logs: Stores application and system logs.
- Container Insights: Provides detailed ECS-level metrics (per task).
- Namespace: Logical grouping of metrics (e.g., AWS/ECS, AWS/ApplicationELB).
- Alarm States: OK, ALARM, INSUFFICIENT_DATA.
- Observability: Combination of metrics, logs, and traces to understand system behavior.

## What I Built Today (Hands-On)
- Created CloudWatch dashboard `flask-app-dashboard`.
- Added widgets:
	- ECS `CpuUtilized` (line graph per service)
	- ECS `MemoryUtilized` (line graph per service) 
	- ALB `RequestCount` (number widget)
	- ALB `HTTPCode_Target_5XX_Count` (number widget)
- Generated traffic using curl loop: 
	- Verified real-time updates in `RequestCount`
- Enabled Container Insights on `project3-cluster`:
	- Observed per-task CPU and memory usage
- Created SNS topic `flask-alerts`:
	- Added and confirmed email subscription
- Created CloudWatch alarm `flask-5xx-errors`:
	- Condition: 5XX errros > 5 in 1 minute
	- Action: Send notification via SNS
- Added alarm status widget to dashboard
- Cleaned up all resources after testing 

## Commands Used 
```bash
for i in {1..30}; do curl http://<alb-dns>/; done
# Generate traffic to test metrics
```

## What Broke / What Confused Me
Nothing broke - But I want to remember: Container Insights is not enabled by default and must be turned on manually to get per-task visibility.

## One-Line Summary 
CloudWatch provides metrics, logs, dashboards, and alerts to monitor application performance and detect issues in real time.

