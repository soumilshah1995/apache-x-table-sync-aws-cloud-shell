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

COPY download URL https://github.com/apache/incubator-xtable/packages/1986830

```agsl
wget -O ./utilities-0.1.0-beta1-bundled.jar "<URL>"

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
