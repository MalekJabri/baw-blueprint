# IBM BAW Blueprint Parser

A specialized toolkit for transforming business documentation into structured IBM Business Automation Workflow (BAW) artifacts using AI-powered document analysis.

## ⚠️ Important Disclaimer

**This is NOT an official IBM project.** This repository contains experimental tools developed using Large Language Models (LLMs) for rapid prototyping and development acceleration.

### Key Considerations:

- **LLM-Generated Content**: All code, assets, and artifacts have been generated or assisted by AI/LLM tools and may contain errors, inconsistencies, or "hallucinations"
- **Not Production-Ready**: These tools are intended for development and testing purposes only
- **Use Standard Mechanisms**: For production environments, we strongly recommend using IBM's official methods:
  - Import BPMN models through standard BAW import
  - Use OpenAPI specifications for service integration
  - Perform manual copy-paste of verified artifacts
  - Follow IBM's official documentation and best practices

### Recommendations:

1. **Always review generated code** before using in any environment
2. **Test thoroughly** in development environments before considering production use
3. **Validate against IBM documentation** and best practices
4. **Use official IBM tools** for production deployments
5. **Consider this as a learning resource** and development accelerator, not a production solution

**By using this repository, you acknowledge that you understand these limitations and will use appropriate caution and validation in your projects.**

---

## 🎯 Project Goals

This toolkit aims to accelerate IBM BAW development by providing:

1. **Process Discovery & BPMN Generation** - AI-powered Blueprint Parser that analyzes business documents to extract processes and automatically generate BPMN designs
2. **Business Object Management** - Tools for extracting, normalizing, and managing business data models from requirements documents
3. **Automated BPMN Creation** - Generate valid BPMN XML files from business process descriptions
4. **Comprehensive Documentation** - Discovery reports, catalogs, and process diagrams

---

## ⚡ Quick Start

Get up and running in 10 minutes!

### 📄 Parse Business Documents

Extract business objects with OpenAPI specs and BPMN processes from documents.

**Time**: ~10 minutes | **Best for**: Complete solution from requirements

**[→ Start with Parse Documents Guide](QUICKSTART_PARSE_DOCUMENTS.md)**

---

## 📋 Table of Contents

- [Quick Start](#-quick-start)
- [Prerequisites](#-prerequisites)
- [Project Structure](#-project-structure)
- [BAW Blueprint Parser Mode](#-baw-blueprint-parser-mode)
- [Getting Started](#-getting-started)
- [Documentation](#-documentation)
- [License](#-license)

---

## 🔧 Prerequisites

### Required Software

#### 1. **IBM Business Automation Workflow (BAW)**
- **Version**: 24.x or higher (25.0.1 recommended)
- **Access**: Process Designer with permissions to import BPMN models
- **Purpose**: Target platform for deploying processes and business objects

#### 2. **Python 3.7+**
- **Purpose**: Business object management and BPMN generation
- **Installation**: [python.org](https://www.python.org/downloads/)
- **Verify**: `python3 --version`

#### 3. **IBM Bob AI Assistant**
- **Purpose**: AI-assisted document parsing and artifact generation
- **Setup**: Configure Bob with BAW Blueprint Parser mode (see `.bob/custom_modes.yaml`)
- **Mode**: Blueprint Parser for document analysis

#### 4. **Modern Web Browser**
- Chrome 85+, Firefox 90+, Safari 14+, or Edge 85+
- **Purpose**: Viewing generated diagrams and reports

### Optional but Recommended

- **Git**: For version control
- **VS Code**: With Bob extension for optimal development experience

---

## 📁 Project Structure

```
BAW_BluePrint/
├── README.md                           # This file
├── QUICKSTART_PARSE_DOCUMENTS.md      # Quick start guide
│
├── business-blueprints/                # Input: Business documents (PDF, DOCX)
│   └── [your-documents].pdf/docx
│
├── business-objects/                   # Output: Business object management
│   ├── generated/                     # Generated business objects by context
│   ├── catalog/                       # Business object catalogs
│   └── reports/                       # Discovery and analysis reports
│
├── business-processes/                 # Output: BPMN process definitions
│   ├── configs/                       # JSON config files for BPMN generation
│   ├── bpmn/                          # Generated BPMN XML files
│   ├── diagrams/                      # Mermaid process diagrams
│   └── catalog/                       # Process catalogs
│
├── BPMN_tools/                        # BPMN generation utilities
│   ├── generate_bpmn.py              # Main BPMN generator
│   ├── bpmn_xml_builder.py           # XML builder
│   ├── CONFIG_SCHEMA_DESIGN.md       # Config schema documentation
│   ├── LLM_USAGE_GUIDE.md            # Guide for LLM usage
│   └── USER_GUIDE.md                 # User guide
│
├── .bob/                              # Bob AI mode configurations
│   ├── custom_modes.yaml             # Mode definitions
│   └── rules-*/                      # Mode-specific instruction files
│
└── docs/                              # Technical documentation
    ├── BAW_BLUEPRINT_PARSER_MODE.md  # Blueprint parser guide
    └── API_REFERENCE.md              # API documentation
```

---

## 🤖 BAW Blueprint Parser Mode

**Slug**: `baw-blueprint-parser`

**Purpose**: Transform business documentation into structured BAW artifacts

### Capabilities

- **Document Parsing**: Analyze business blueprint documents (PDF, Word, etc.)
- **Entity Extraction**: Extract business entities, fields, and relationships
- **Process Discovery**: Discover business processes and workflows from text
- **Business Objects**: Generate JSON business object definitions with OpenAPI specs
- **BPMN Generation**: Create BPMN configuration files (JSON) and valid BPMN XML
- **Process Diagrams**: Generate Mermaid process diagrams for visualization
- **Documentation**: Create discovery reports and catalogs
- **Registration**: Register business objects with deterministic class IDs

### When to Use

- Analyzing business requirements documents
- Extracting data models from specifications
- Discovering business processes from descriptions
- Preparing artifacts for BAW import

### Output Structure

```
business-objects/
├── generated/
│   └── [context]/
│       ├── [EntityName].json          # Business object definitions
│       └── [EntityName]_openapi.json  # OpenAPI specifications
├── catalog/
│   └── business_objects_catalog.json  # Complete catalog
└── reports/
    └── discovery_report_[context].md  # Analysis report

business-processes/
├── configs/
│   └── [context]/
│       └── [ProcessName]_config.json  # BPMN configuration
├── bpmn/
│   └── [context]/
│       └── [ProcessName].bpmn         # BPMN XML file
├── diagrams/
│   └── [context]/
│       └── [ProcessName].md           # Mermaid diagram
└── catalog/
    └── process_catalog.json           # Process catalog
```

**📖 Detailed Documentation**: [`docs/BAW_BLUEPRINT_PARSER_MODE.md`](docs/BAW_BLUEPRINT_PARSER_MODE.md)

---

## 🚀 Getting Started

### Quick Start Guide

#### 1. **Clone the Repository**
```bash
git clone <repository-url>
cd BAW_BluePrint
```

#### 2. **Install Python Dependencies**
```bash
pip install -r requirements.txt  # If requirements.txt exists
```

#### 3. **Configure Bob Modes**
The Blueprint Parser mode is pre-configured in `.bob/custom_modes.yaml`. Ensure Bob AI is installed and configured.

#### 4. **Parse Business Documents**

**Step 1**: Place your business documents in `business-blueprints/`
```bash
# Supported formats: PDF, DOCX
cp your-document.pdf business-blueprints/
```

**Step 2**: Activate Blueprint Parser Mode
```
Ask Bob: "Switch to BAW Blueprint Parser mode"
```

**Step 3**: Parse the Document
```
Request: "Parse [document-name] and generate business objects and processes"
```

**Step 4**: Review Generated Artifacts
- Business objects: `business-objects/generated/[context]/`
- BPMN configs: `business-processes/configs/[context]/`
- BPMN XML: `business-processes/bpmn/[context]/`
- Reports: `business-objects/reports/`
- Catalogs: `business-objects/catalog/` and `business-processes/catalog/`

**Step 5**: Import into BAW
- Import BPMN XML files through BAW Process Designer
- Use standard BAW import mechanisms for business objects
- Follow IBM's official documentation for deployment

---

## 📚 Documentation

### Technical Documentation (`docs/`)
- **[BAW_BLUEPRINT_PARSER_MODE.md](docs/BAW_BLUEPRINT_PARSER_MODE.md)** - Complete guide to Blueprint Parser mode
- **[API_REFERENCE.md](docs/API_REFERENCE.md)** - API documentation

### BPMN Tools Documentation (`BPMN_tools/`)
- **[README.md](BPMN_tools/README.md)** - BPMN tools overview
- **[CONFIG_SCHEMA_DESIGN.md](BPMN_tools/CONFIG_SCHEMA_DESIGN.md)** - Configuration schema
- **[LLM_USAGE_GUIDE.md](BPMN_tools/LLM_USAGE_GUIDE.md)** - Guide for LLM-based generation
- **[USER_GUIDE.md](BPMN_tools/USER_GUIDE.md)** - User guide for BPMN generation

---

## 🔄 Typical Workflow

### Parse Business Documents and Generate BPMN

```
1. Place PDF/Word documents in business-blueprints/
2. Bob: "Switch to BAW Blueprint Parser mode"
3. You: "Parse [DocumentName] and generate business objects and processes"
4. Bob: Extracts entities, creates JSON files, generates BPMN configs
5. Bob: Automatically generates BPMN XML files
6. You: Review generated artifacts in respective directories
7. You: Import BPMN XML into BAW Process Designer
8. You: Register business objects in BAW using standard methods
```

### Example Commands

**Parse a specific document:**
```
"Parse Cross-Border_Payments_South_Africa.docx and extract all business entities and processes"
```

**Generate BPMN from existing config:**
```
"Generate BPMN XML from the payment_approval_config.json"
```

**Create process catalog:**
```
"Create a catalog of all discovered processes"
```

---

## 🎨 Best Practices

### Document Parsing
1. Use well-structured business documents with clear sections
2. Ensure documents contain explicit process descriptions
3. Include data models and entity relationships
4. Provide context about business rules and validations

### Business Object Management
1. Use consistent naming conventions (PascalCase)
2. Register objects with deterministic class IDs
3. Document assumptions in discovery reports
4. Organize by business context
5. Validate references and relationships

### BPMN Generation
1. Review generated BPMN configs before XML generation
2. Validate BPMN XML against BAW requirements
3. Test processes in development environment first
4. Document process assumptions and business rules
5. Use Mermaid diagrams for stakeholder communication

---

## 🤝 Contributing

When adding to this toolkit:

1. Follow established directory structures
2. Include comprehensive documentation
3. Test across supported BAW versions
4. Update relevant catalogs and indexes
5. Document any assumptions or limitations

---

## 📄 License

```
Licensed Materials - Property of IBM
5725-C95
(C) Copyright IBM Corporation 2025-2026
```

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

---

## 📞 Support

### Documentation
- Blueprint Parser: `docs/BAW_BLUEPRINT_PARSER_MODE.md`
- BPMN Tools: `BPMN_tools/README.md`
- Quick Start: `QUICKSTART_PARSE_DOCUMENTS.md`

### IBM Resources
- [IBM BAW Documentation](https://www.ibm.com/docs/en/baw)
- [BPMN 2.0 Specification](https://www.omg.org/spec/BPMN/2.0/)

### Troubleshooting
- Verify document format is supported (PDF, DOCX)
- Check Python version compatibility
- Review mode-specific documentation
- Validate generated BPMN against BAW requirements

---

**Version**: 1.0.0  
**Last Updated**: June 2026  
**BAW Compatibility**: v24.x, v25.x  
**Focus**: Business Blueprint Parsing & BPMN Generation

---

**Ready to start?**
- 📄 [Parse Your First Document](QUICKSTART_PARSE_DOCUMENTS.md)
- 📘 [Learn About Blueprint Parser Mode](docs/BAW_BLUEPRINT_PARSER_MODE.md)
- 🔧 [Explore BPMN Tools](BPMN_tools/README.md)
