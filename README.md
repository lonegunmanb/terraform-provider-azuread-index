# Terraform Provider AzureAD Index

An automated indexing system that generates comprehensive indexes for the HashiCorp Terraform AzureAD provider, enabling AI agents, IDEs, and development tools to better understand and work with Terraform provider code.

## 🎯 Purpose

This repository automatically monitors the [`hashicorp/terraform-provider-azuread`](https://github.com/hashicorp/terraform-provider-azuread) repository for new releases and generates structured indexes containing:

- **Terraform Resources** (e.g., `azuread_application`, `azuread_group`)
- **Data Sources** (e.g., `azuread_client_config`, `azuread_domains`)
- **Ephemeral Resources** (e.g., `azuread_application_password`)
- **Go Symbol Information** (functions, types, methods)
- **CRUD Method Mappings** (Create, Read, Update, Delete operations)

## 📁 Index File Organization

The generated indexes are organized in a structured directory layout:

```text
index/
├── terraform-provider-azuread-index.json     # Master index with metadata
├── resources/                               # Individual resource mappings
│   ├── azuread_application.json
│   ├── azuread_group.json
│   ├── azuread_user.json
│   └── ... (50+ resource files)
├── datasources/                             # Individual data source mappings
│   ├── azuread_client_config.json
│   ├── azuread_domains.json
│   ├── azuread_application.json
│   └── ... (40+ data source files)
├── ephemeral/                               # Individual ephemeral resource mappings
│   ├── azuread_application_password.json
│   ├── azuread_service_principal_password.json
│   └── ... (ephemeral resource files)
└── internal/                                # Go symbol indexes (if enabled)
    ├── func.NewSomething.goindex
    ├── type.SomeType.goindex
    └── ... (Go function/type indexes)
```

### Index File Structure

Each resource/data source/ephemeral resource has its own JSON file containing:

#### Resource Example (`resources/azuread_application.json`)

```json
{
  "terraform_type": "azuread_application",
  "struct_type": "",
  "namespace": "github.com/hashicorp/terraform-provider-azuread/internal/services/applications",
  "registration_method": "resourceApplication",
  "sdk_type": "legacy_pluginsdk",
  "schema_index": "func.resourceApplication.goindex",
  "create_index": "func.resourceApplicationCreate.goindex",
  "read_index": "func.resourceApplicationRead.goindex",
  "update_index": "func.resourceApplicationUpdate.goindex",
  "delete_index": "func.resourceApplicationDelete.goindex",
  "attribute_index": "func.resourceApplication.goindex"
}
```

#### Data Source Example (`datasources/azuread_client_config.json`)

```json
{
  "terraform_type": "azuread_client_config",
  "struct_type": "",
  "namespace": "github.com/hashicorp/terraform-provider-azuread/internal/services/authentication",
  "registration_method": "dataSourceClientConfig",
  "sdk_type": "legacy_pluginsdk",
  "schema_index": "func.dataSourceClientConfig.goindex",
  "read_index": "func.dataSourceClientConfigRead.goindex",
  "attribute_index": "func.dataSourceClientConfig.goindex"
}
```

#### Ephemeral Resource Example (`ephemeral/azuread_application_password.json`)

```json
{
  "terraform_type": "azuread_application_password",
  "struct_type": "ApplicationPasswordEphemeralResource",
  "namespace": "github.com/hashicorp/terraform-provider-azuread/internal/services/applications",
  "registration_method": "EphemeralResources",
  "sdk_type": "ephemeral",
  "schema_index": "method.ApplicationPasswordEphemeralResource.Schema.goindex",
  "open_index": "method.ApplicationPasswordEphemeralResource.Open.goindex",
  "renew_index": "method.ApplicationPasswordEphemeralResource.Renew.goindex",
  "close_index": "method.ApplicationPasswordEphemeralResource.Close.goindex"
}
```

## 🚀 Usage Examples

### For AI Agents and Language Models

#### 1. Finding Resource Implementation Details

```bash
# Get information about azuread_application resource
curl https://raw.githubusercontent.com/lonegunmanb/terraform-provider-azuread-index/main/index/resources/azuread_application.json
```

#### 2. Discovering Available Resources

```bash
# List all available resources
curl https://api.github.com/repos/lonegunmanb/terraform-provider-azuread-index/contents/index/resources
```

#### 3. Finding CRUD Methods for Development

```bash
# Get CRUD method names for azuread_group
curl https://raw.githubusercontent.com/lonegunmanb/terraform-provider-azuread-index/main/index/resources/azuread_group.json | jq '.create_index, .read_index, .update_index, .delete_index'
```

### Supported Provider Versions

- **Latest Stable**: Always tracks the latest stable release (from `v2.53.1`)
- **Version History**: Tagged releases match the upstream provider versions
- **SDK Support**: Handles both Legacy Plugin SDK and Modern Terraform Plugin Framework

## 🛠️ Technical Architecture

### Multi-SDK Support

- **Legacy Plugin SDK**: Resources using `pluginsdk.Resource` structs
- **Modern Framework**: Resources using the newer Terraform Plugin Framework
- **Ephemeral Resources**: Temporary resources with Open/Renew/Close lifecycle

### Progress Tracking

Rich progress bars with:

- 🔄 Real-time progress indicators
- 📊 Completion percentages and item counts
- ⏱️ Elapsed time and ETA calculations
- ⚡ Processing rates (items/second)

## 📊 Statistics

Based on the latest Terraform Provider AzureAD version:

- **🏗️ Resources**: ~50 Terraform resources (e.g., `azuread_application`, `azuread_group`)
- **📖 Data Sources**: ~40 data sources (e.g., `azuread_client_config`, `azuread_domains`)
- **⚡ Ephemeral Resources**: ~5 ephemeral resources (e.g., `azuread_application_password`)
- **📦 Services**: 15 Azure AD service packages (e.g., `applications`, `groups`, `users`)
- **🔧 SDK Types**: Legacy Plugin SDK, Modern Framework, and Ephemeral support

## 🤝 Contributing

This repository is automatically maintained, but contributions are welcome:

1. **Bug Reports**: File issues for incorrect or missing index information
2. **Feature Requests**: Suggest improvements to the indexing system
3. **Tool Integration**: Share examples of how you're using these indexes

## 📄 License

This project is licensed under the same terms as the HashiCorp Terraform Provider AzureAD (Mozilla Public License 2.0).

## 🔗 Related Projects

- [HashiCorp Terraform Provider AzureAD](https://github.com/hashicorp/terraform-provider-azuread) - The source provider being indexed
- [Terraform](https://terraform.io) - Infrastructure as Code tool
- [Gophon](https://github.com/lonegunmanb/gophon) - Go symbol indexing tool (if used for additional Go indexes)
- [`terraform-mcp-eva`](https://github.com/lonegunmanb/terraform-mcp-eva) - An experimental MCP serer that helps Terraform module developers to make their life easier.