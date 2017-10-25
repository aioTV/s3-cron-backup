# s3-cron-backup
Docker container for backing up to S3 based on a cron schedule

## Environment Variables
This image extends [xueshanf/awscli](https://hub.docker.com/r/xueshanf/awscli/) so all
variables that can be set in that image apply here.

```
CRON_SCHEDULE - Default to "* * * * *" - The schedule at which to run the backup, used by crond
S3_BUCKET_URL - The S3 path to upload the compressed backup file to
BACKUP_NAME - Default to "backup" - The prefix for the backup file, file is named ${BACKUP_NAME}-$(date -u +"%Y-%m-%dT%H:%M:%SZ").tar.gz
BACKUP_DIR - The directory inside of the container to backup
```

## Usage
Example command for docker run:
```
docker run -d -e S3_BUCKET_URL="s3://foo/bar" -e BACKUP_DIR=/jenkins_home -v "$(pwd)/jenkins_home:/jenkins_home:ro" aiotv/s3-cron-backup
```
