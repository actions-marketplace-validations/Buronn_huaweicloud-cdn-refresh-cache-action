# Huawei CDN Refresh Cache Action

## Overview
The **Huawei CDN Refresh Cache Action** is a GitHub Action that allows users to refresh the cache on Huawei Cloud CDN. This action supports both file and directory cache purging with configurable refresh modes.

## Inputs

| Name | Description | Required | Default |
|------|-------------|----------|---------|
| `access_key_id` | Huawei Cloud Access Key ID. | Yes | N/A |
| `secret_access_key` | Huawei Cloud Secret Access Key. | Yes | N/A |
| `region` | Region ID (e.g., `cn-north-1` for Chinese Mainland, `ap-southeast-1` for International). | Yes | N/A |
| `enterprise_project_id` | ID of the enterprise project to which the cache purge task is added. Required for IAM users. | No | N/A |
| `type` | Type of resource to refresh cache (`file` or `directory`). | No | `file` |
| `mode` | Refresh mode (`all` or `detect_modify_refresh`). | No | `all` |
| `zh_url_encode` | Whether to encode the URL in Chinese (`true` or `false`). | No | `false` |
| `urls` | A comma-separated list of URLs to refresh. Must include `http://` or `https://`. Up to 1,000 URLs or 100 directories allowed. | Yes | N/A |

## Usage Example

```yaml
title: Example Workflow
name: Refresh Huawei CDN Cache
on:
  push:
    branches:
      - main

jobs:
  refresh-cache:
    runs-on: ubuntu-latest
    steps:
    - name: Huawei CDN Refresh Cache
      uses: Buronn/huaweicloud-cdn-refresh-cache-action@v1.0.0
      with:
        access_key_id: ${{ secrets.HUAWEI_ACCESS_KEY_ID }}
        secret_access_key: ${{ secrets.HUAWEI_SECRET_ACCESS_KEY }}
        region: ${{ vars.HUAWEI_REGION }}
        type: "directory"
        urls: ${{ vars.URLS }}
```

## How It Works
1. **Authentication**: The action authenticates using Huawei Cloud Access Key and Secret Access Key.
2. **Setup KooCLI**: It installs the Huawei Cloud CLI (KooCLI) for API interactions.
3. **Cache Refresh Execution**: It triggers a cache refresh task for the specified URLs or directories.

## Notes
- Ensure that the provided `access_key_id` and `secret_access_key` have the necessary permissions to perform cache refresh operations.
- Use `enterprise_project_id` only if your Huawei Cloud account has enterprise projects enabled.

## License
This action is licensed under the [MIT License](LICENSE).