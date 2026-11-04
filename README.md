
# AWS CloudWatch Monitoring & SNS Alert Lab

## Project Overview
Built and tested an AWS monitoring solution that tracks EC2 CPU utilization, detects high CPU usage through Amazon CloudWatch, and sends automated email notifications using Amazon SNS.

**Project Status:** Successfully completed — November 4, 2026

## AWS Services and Tools
- Amazon EC2 — Amazon Linux 2023, t3.micro instance
- Amazon CloudWatch — CPU monitoring, metrics, and alarms
- Amazon SNS — Automated email notifications
- Linux — EC2 Instance Connect and command-line workload testing

## Architecture
EC2 Instance → CloudWatch CPU Metric → CloudWatch Alarm → Amazon SNS → Email Notification

## Implementation
1. Launched an Amazon Linux 2023 EC2 instance named `cloudwatch-monitoring-lab` in the US East (Ohio) region.
2. Verified that the instance was running and connected using EC2 Instance Connect.
3. Examined CPU utilization and performance metrics in CloudWatch.
4. Created the alarm `EC2-High-CPU-70-Percent` using the `AWS/EC2` CPUUtilization metric.
5. Configured the alarm to evaluate average CPU utilization over a 5-minute period, with a threshold greater than 70% and 1 out of 1 datapoints required.
6. Configured an SNS email notification action for the alarm.
7. Generated a controlled CPU workload using Linux to test the alarm.
8. Reviewed CloudWatch alarm history and verified delivery of the SNS email.
9. Stopped the EC2 instance after testing to avoid unnecessary compute charges.

## CPU Stress Test
Executed the following command to create a CPU-intensive workload on both vCPUs, with an automatic timeout of 420 seconds:

```bash
timeout 420 bash -c 'yes > /dev/null & yes > /dev/null & wait'
```

## Verified Results

| Measurement | Result |
|---|---|
| CPU alarm threshold | Greater than 70% |
| Observed CPU utilization | 80.54% |
| Alarm transition | OK → ALARM |
| Alarm triggered | November 4, 2026, 06:45:46 UTC |
| SNS notification | Successfully executed and email received |
| Alarm recovery | ALARM → OK at 06:50:46 UTC |
| Final test outcome | PASS |

## Troubleshooting and Lessons Learned
The initial short CPU workload did not produce a confirmed alarm transition. After reviewing the five-minute alarm evaluation period, I performed a longer, controlled CPU stress test. CloudWatch then detected a qualifying CPU datapoint and triggered the alarm and SNS notification.

This project demonstrates practical experience with EC2 administration, CloudWatch monitoring, alarm thresholds, SNS integration, Linux testing, alarm history verification, and AWS resource management.

## Evidence
CloudWatch alarm history and SNS notification screenshots will be added after redacting account identifiers and other sensitive information.

## Cost Awareness
Stopped the EC2 instance after testing. CloudWatch alarms, detailed monitoring, and other AWS resources may still incur charges independently of EC2 compute usage.
