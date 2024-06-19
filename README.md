# apache-x-table-sync-aws-cloud-shell
apache-x-table-sync-aws-cloud-shell


# Apache X Table Sync on AWS Cloud Shell

This guide will walk you through the steps to run Apache X Table Sync on AWS Cloud Shell.

## Prerequisites

Before you begin, ensure you have the following:

- AWS account with appropriate permissions
- AWS access key ID and secret access key
- AWS region set to `us-east-1` (or adjust as needed)

## Steps

1. **Create a Directory**:

   ```bash
   mkdir xtable
   cd xtable
   ```

2. set aws cred 
```
export AWS_ACCESS_KEY_ID=XX
export AWS_SECRET_ACCESS_KEY=XX
export AWS_REGION=us-east-1
```

Install Java:

bash
```
sudo yum install java
```

Download Apache X Table Sync JAR:
```agsl
wget -O ./utilities-0.1.0-beta1-bundled.jar "https://github-registry-files.githubusercontent.com/669267591/3a589880-82aa-11ee-9533-12d8e3ced2b9?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240619%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240619T132444Z&X-Amz-Expires=300&X-Amz-Signature=96d71e313ea1beb9e49af3fefd239f0715ee7d24801825cec5a0e64798a13597&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=669267591&response-content-disposition=filename%3Dutilities-0.1.0-beta1-bundled.jar&response-content-type=application%2Foctet-stream"

```

Create Configuration File:

Create  my_config.yaml file and add the following configuration:
```
sourceFormat: HUDI

targetFormats:
  - ICEBERG

datasets:
  -
    tableBasePath: s3://XX/xmldata/silver/table_name=invoices/
    tableName: invoices
    partitionSpec: destinationstate:VALUE

```

Run Apache X Table Sync:
```
java -jar  ./utilities-0.1.0-beta1-bundled.jar --dataset ./my_config.yaml
```
