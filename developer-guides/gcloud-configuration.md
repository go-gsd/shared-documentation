# Google Cloud CLI Configuration

This guide provides step-by-step instructions for setting up and configuring the Google Cloud CLI (gcloud).

## Prerequisites

### Installing the gcloud CLI

To set up the gcloud CLI, follow the steps in [Install the gcloud CLI](https://cloud.google.com/sdk/docs/install).

### Creating a New Configuration

After installing the gcloud CLI, create a new configuration to manage your settings:

```bash
gcloud config configurations create my-config
```

Set the required project and account:

```bash
gcloud config set project YOUR_PROJECT_ID
gcloud config set account your-email@example.com
```

Optionally, set the default region and zone:

```bash
gcloud config set compute/region YOUR_REGION
gcloud config set compute/zone YOUR_ZONE
```

## Configuration Steps

### 1. Initial Authentication

After installing gcloud CLI, you need to authenticate with Google Cloud:

```bash
gcloud auth login
```

This command opens a web browser where you can sign in to your Google account and authorize the gcloud CLI.

### 2. Application Default Credentials

For applications that use Google Cloud client libraries, set up application default credentials:

```bash
gcloud auth application-default login
```

This is essential for applications that need to authenticate with Google Cloud services programmatically.

## Configuration Management

### View Current Configuration

Check your current gcloud configuration:

```bash
gcloud config list
```

### Create Named Configurations

For managing multiple environments, create named configurations:

```bash
gcloud config configurations create dev-environment
gcloud config configurations create prod-environment
```

Switch between configurations:

```bash
gcloud config configurations activate dev-environment
```

### Modify Existing Configuration Properties

To update properties of an existing configuration:

```bash
gcloud config set core/disable_usage_reporting true
gcloud config set core/disable_prompts true
```

## Verification

### Test Your Configuration

Verify your authentication and project access:

```bash
gcloud auth list
gcloud projects list
gcloud compute instances list
```

### Check IAM Permissions

Ensure you have the necessary IAM permissions for the resources you need to access:

```bash
gcloud projects get-iam-policy YOUR_PROJECT_ID
```

## Best Practices

1. **Use Named Configurations**: Create separate configurations for different environments (dev, staging, prod)
2. **Set Default Project**: Always set a default project to avoid repetitive --project flags
3. **Application Default Credentials**: Set up ADC for applications that use Google Cloud client libraries
4. **Regular Authentication**: Refresh your authentication tokens regularly using `gcloud auth login`
5. **Verify Permissions**: Ensure you have the necessary IAM permissions for your Google Cloud resources

## Troubleshooting

### Authentication Issues

If you encounter authentication problems:

```bash
gcloud auth revoke
gcloud auth login
gcloud auth application-default login
```

### Project Access Issues

Verify you have access to the project:

```bash
gcloud projects describe YOUR_PROJECT_ID
```
