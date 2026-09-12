# Linux SIEM & Threat Detection Lab

A hands-on SIEM lab built with **Kali Linux, Filebeat, Elasticsearch and Kibana**.

## Architecture

```text
Kali Linux VM
   | /var/log/auth.log
   v
 Filebeat
   | HTTP :9200
   v
Elasticsearch 7.17.10
   | :5601
   v
Kibana 7.17.10
   +-- Discover / Investigation
   +-- Mini-SIEM Security Dashboard
   +-- Threshold Rules
   +-- Index Connector
```

## Technologies

- Kali Linux
- Filebeat 7.17.10
- Elasticsearch 7.17.10
- Kibana 7.17.10
- Docker Desktop / WSL2
- Windows host

## Dashboard

The Dashboard contains:

1. Authentication Failure Over Time
2. Sudo Activity Over Time
3. User Activity
4. Authentication Failures by Process
5. Authentication Failure Details
6. Total Authentication Failures

Index pattern: `filebeat-*`  
Time field: `@timestamp`

A scripted field named `auth_user` was used to extract usernames from authentication-failure messages where the username was embedded in `message`.

## Security scenarios tested

- Successful and failed `su`
- SSH authentication success/failure
- Sudo activity
- Unauthorized sudo attempts
- Session open/close events
- Multiple test users: Vijay, Arch and Misty

## Alerting

Two Index Threshold rules were created:

- **High Filebeat Event Volume**
- **Unusual User Activity**

The rules successfully detected threshold conditions. An Index connector named **SIEM Alert Index** was configured for the `siem-alerts` index and was independently verified through manual testing.

### Known limitation

In this Kibana 7.17 lab, **Unusual User Activity** reached an Active / Threshold met state, but its automatic Index action did not consistently create a new document in `siem-alerts`. The connector itself worked when tested manually. This is documented as a lab limitation rather than claimed as a successful automatic notification.

## Persistence

Elasticsearch uses the named Docker volume:

`minisIem_elasticsearch_data`

A local Elasticsearch backup was maintained during development but is intentionally excluded from this public repository.

## Troubleshooting

The project involved resolving:

- Windows/Kali network connectivity
- Filebeat output connectivity
- Elasticsearch persistence
- Kibana saved-object persistence
- incorrect Kali timezone
- Filebeat ingestion verification
- Kibana alerting/connector behavior

## Learning outcome

This project demonstrates the SIEM workflow:

**Endpoint logs → collection → centralized storage → investigation → visualization → detection**
