# Quick Start: BAW Blueprint Parser Mode

## 🚀 5-Minute Quick Start

### Step 1: Activate Mode
```
Ask Bob: "Switch to BAW Blueprint Parser mode"
```

### Step 2: Analyze Your Document
```
Ask Bob: "Please review the [YourDocument] and generate BPMN and business objects"
```

### Step 3: Review Generated Files
- **Business Objects:** `business-objects/generated/[Context]/`
- **BPMN Config:** `business-processes/configs/[Context]/`
- **BPMN Files:** `business-processes/bpmn/[Context]/`

### Step 4: View BPMN
Open `*-preview.bpmn` in [bpmn.io](https://demo.bpmn.io/)

---

## 📋 Common Commands

### Generate from Blueprint
```
"Review [document] and provide BPMN and business objects"
```

### Regenerate BPMN
```bash
python3 BPMN_tools/generate_bpmn.py \
  business-processes/configs/[Context]/[Process].bpmn-config.json \
  business-processes/bpmn/[Context]/[Process].bpmn
```

### View Generated Artifacts
```bash
# List business objects
ls business-objects/generated/[Context]/

# List BPMN files
ls business-processes/bpmn/[Context]/

# View catalogs
cat business-objects/catalog/[Context].catalog.json
```

---

## 🎯 What Gets Generated

### For Each Blueprint Document:

**Business Objects** (JSON)
- One file per entity
- Complete property definitions
- Relationships documented

**BPMN Process** (2 formats)
- IBM BAW version (`.bpmn`)
- Standard BPMN 2.0 preview (`-preview.bpmn`)

**Catalogs** (JSON)
- Business object catalog
- Process catalog
- OpenAPI specification

**Documentation**
- Templates for future use
- Enhancement guides

---

## ✅ Validation Checklist

### Business Objects
- [ ] Type is `"businessObject"`
- [ ] Properties have name, type, required, description
- [ ] Relationships are clear
- [ ] Enums defined where needed

### BPMN Process
- [ ] Opens without errors in viewer
- [ ] All lanes have consistent width
- [ ] Activities properly connected
- [ ] Gateways have conditions
- [ ] Start and end events present

### Catalogs
- [ ] All objects listed
- [ ] Relationships documented
- [ ] Metadata complete

---

## 🔧 Quick Fixes

### Fix: "Not a businessObject type"
```json
Change: "type": "complex"
To:     "type": "businessObject"
```

### Fix: Properties Format Error
Use array format:
```json
"properties": [
  { "name": "id", "type": "String", "required": true }
]
```

### Fix: Gateway Direction Error
Regenerate BPMN files (auto-fixed in latest version)

---

## 📚 Full Documentation

- **Complete Lab:** [`LAB_BAW_BLUEPRINT_PARSER.md`](LAB_BAW_BLUEPRINT_PARSER.md)
- **BO Template:** [`BUSINESS_OBJECT_TEMPLATE.md`](BUSINESS_OBJECT_TEMPLATE.md)
- **Mode Reference:** [`BAW_BLUEPRINT_PARSER_MODE.md`](BAW_BLUEPRINT_PARSER_MODE.md)
- **BPMN Tools:** [`../BPMN_tools/USER_GUIDE.md`](../BPMN_tools/USER_GUIDE.md)

---

## 💡 Pro Tips

1. **Structure Your Documents**
   - Clear section headings
   - Structured entity descriptions
   - Step-by-step process flows

2. **Iterate Quickly**
   - Generate → Review → Modify → Regenerate

3. **Use Templates**
   - Reference templates for consistency
   - Copy-paste for new objects

4. **Validate Early**
   - Open BPMN in viewer immediately
   - Check business object format

5. **Version Control**
   - Commit generated files
   - Tag releases
   - Document changes

---

## 🎓 Example Session

```
You: "Switch to BAW Blueprint Parser mode"
Bob: ✅ Switched to BAW Blueprint Parser mode

You: "Review Cross-Border_Payments_South_Africa.docx and generate artifacts"
Bob: 📖 Reading document...
     ✅ Generated 8 business objects
     ✅ Generated BPMN config
     ✅ Generated BPMN XML files
     ✅ Created catalogs

You: "Open the preview BPMN in bpmn.io"
[View beautiful process diagram with consistent lanes]

You: "Perfect! Now package for deployment"
Bob: 💼 Ready to switch to BAW Package Manager mode...
```

---

**Need Help?** Refer to the [Complete Lab Guide](LAB_BAW_BLUEPRINT_PARSER.md) for detailed instructions.

**Version:** 1.0.0 | **Updated:** 2026-06-18