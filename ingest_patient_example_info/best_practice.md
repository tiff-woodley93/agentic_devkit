1. MinIO Bucket Setup:

Add bucket creation to docker-compose
Upload CSVs to minio during container entrypoint

2. Raw Layer (models/raw/):

External models for each CSV
Materialize as tables named <filename>_csv

3. Staging Layer (models/staging/):

Source from raw models
Apply standardizations (snake_case, type casting, null filtering)

4. Update schema contract

Make sure to update the schema_contract in the agentic_devkit to align with the schema of the postgres database

Deliverables:

Python ingestion script
dbt models/config
README with execution/setup instructions