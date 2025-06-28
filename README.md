# Elastic Beanstalk Worker Environment with Cron Job

A Python WSGI application for AWS Elastic Beanstalk with worker environment support and automated cron job scheduling.

## Features

- Python WSGI application with SQS message processing
- Worker environment support for background tasks
- Automated cron job setup via .ebextensions
- Logging to console for CloudWatch integration

## Files

- `application.py` - Main WSGI application
- `.ebextensions/cron.config` - Cron job configuration
- Pre-built deployment packages (zip files)

## Deployment Instructions

### Option 1: Using Pre-built Package

1. Download `elastic-beanstalk-app-with-cron.zip`
2. Go to AWS Elastic Beanstalk Console
3. Create new application or select existing one
4. Choose "Worker environment" as environment tier
5. Upload the zip file
6. Deploy

### Option 2: Build from Source

1. Clone this repository:
   ```bash
   git clone https://github.com/pravinmenghani1/elastic-beanstalk-worker-env.git
   cd elastic-beanstalk-worker-env
   ```

2. Create deployment package:
   ```bash
   zip -r app.zip application.py .ebextensions/
   ```

3. Deploy to Elastic Beanstalk:
   - Upload `app.zip` to your Elastic Beanstalk environment
   - Ensure environment tier is set to "Worker"

## Cron Job Verification

After deployment, verify the cron job is working:

1. SSH into your EC2 instance
2. Check the cron log:
   ```bash
   tail -f /tmp/cronlog.txt
   ```

## Application Endpoints

- `GET /` - Returns welcome page
- `POST /` - Processes SQS messages
- `POST /scheduled` - Handles scheduled tasks

## Environment Requirements

- AWS Elastic Beanstalk
- Python 3.x platform
- Worker environment tier
- SQS queue (for message processing)