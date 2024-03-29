# GitHub Action to upload files to Azure Blob Storage containers

This action is designed to use the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) to upload files from a local directory an Azure Blob Storage container.

## Usage

### Example

Place in a `.yml` file such as this one in your `.github/workflows` folder. [Refer to the documentation on workflow YAML syntax here.](https://help.github.com/en/articles/workflow-syntax-for-github-actions)

```yaml
name: Upload Files To Azure Blob Storage
on:
  push:
    branches:
      - master
jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: karlsgate/azure-blob-upload@v4
        with:
          source_directory: _dist
          container_name: www
          connection_string: ${{ secrets.ConnectionString }}
          pattern: '*.tar.gz'
          content_type: application/x-tar
          overwrite: true
```

### Required Variables

| Key                 | Value                                                                    |
|---------------------|--------------------------------------------------------------------------|
| `source_directory`  | The local directory containing the files to upload                       |
| `container_name`    | The name of the destination storage account container                    |
| `connection_string` | The connection string with SAS token for the destination storage account |

### Optional Variables

| Key            | Value                                                                              |
|----------------|------------------------------------------------------------------------------------|
| `pattern`      | An optional file pattern to limit the files uploaded from the source directory     |
| `content_type` | An optional content type explicitly set for the uploaded files                     |
| `overwrite`    | An optional boolean to overwrite existing files in the destination storage account |

## License

This project is distributed under the [MIT License](LICENSE.md).
