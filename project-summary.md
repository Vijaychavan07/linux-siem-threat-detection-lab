# Linux SIEM & Threat Detection Lab — Brief Project Summary

## Objective
Build a small SIEM environment for collecting and investigating Linux authentication events.

## Architecture
Kali Linux VM → Filebeat → Elasticsearch 7.17.10 → Kibana 7.17.10.

Elasticsearch and Kibana run in Docker Desktop/WSL2 on Windows. Filebeat on Kali sends authentication logs to the Windows host.

## Data Source
`/var/log/auth.log`, collected through the Filebeat System module.

## Dashboard
Six visualizations cover authentication failures, sudo activity, user activity, processes and authentication-failure details.

## Detection
Two Index Threshold rules were created: High Filebeat Event Volume and Unusual User Activity. Both were observed detecting threshold conditions.

## Alert connector
The SIEM Alert Index connector was manually verified to write documents to `siem-alerts`. Automatic action from the grouped Unusual User Activity rule remained a known Kibana 7.17 limitation in this lab.

## Persistence
Elasticsearch uses the `minisIem_elasticsearch_data` Docker volume.

## Testing
The lab used successful/failed `su`, SSH activity, sudo activity, unauthorized sudo attempts and multiple test users.

## Key troubleshooting
Networking, Elasticsearch persistence, Kibana saved objects, Filebeat connectivity and endpoint timezone configuration were resolved during development.

## Learning outcome
Hands-on experience with Linux security logs, log shipping, centralized storage, SIEM investigation, dashboards, threshold detection and troubleshooting.
