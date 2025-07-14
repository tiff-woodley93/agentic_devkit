Ingest csv data into minio and then into a postgres database using the following steps:

1. Source Folder to MinIO Upload

Read CSVs from ./src/data
Upload to MinIO bucket raw-csv using boto3
Use correct text/csv content-type and retain filenames
2. dbt Integration to Pull and Transform

Define external tables using MinIO S3 endpoint
Stage to Postgres staging schema
Transform: rename to snake_case, filter null PKs, cast dates
Use source definitions
3. Postgres Loading

Load transformed data to analytics schema
Add basic tests (not_null, unique)
Additional:

Use .env for secrets
Pipeline should be idempotent
Log errors/progress
Deliverables:

Python script for ingestion
dbt models and config
README with usage/setup instructions