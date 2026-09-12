# Run Notes

1. Create a local `.env` from `filebeat/.env.example` and set a private encryption key.
2. Start Elasticsearch/Kibana with `docker compose up -d`.
3. On Kali, adapt `filebeat.yml` and replace `ELASTICSEARCH_HOST` with the Windows host IP.
4. Enable the Filebeat System module using `system.yml`.
5. In Kibana, create the `filebeat-*` index pattern using `@timestamp`.
