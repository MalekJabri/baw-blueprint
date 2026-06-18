# Business Object Template and Format Guide

This document provides the correct format for creating business objects that are compatible with the BAW Blueprint Parser mode and the business object scanner.

## Critical Format Requirements

### 1. Type Field
**MUST** be set to `"businessObject"`:
```json
{
  "type": "businessObject"
}
```

❌ **WRONG:** `"type": "complex"`, `"type": "object"`, or any other value

### 2. Properties Format
**MUST** be an **array** of property objects, not a dictionary:

✅ **CORRECT:**
```json
{
  "properties": [
    {
      "name": "propertyName",
      "type": "String",
      "required": true,
      "description": "Property description"
    }
  ]
}
```

❌ **WRONG:**
```json
{
  "properties": {
    "propertyName": {
      "type": "string",
      "required": true
    }
  }
}
```

### 3. Type Names
Use **BAW type names** (PascalCase), not JSON Schema types:

| ✅ Correct | ❌ Wrong |
|-----------|---------|
| `String` | `string` |
| `Integer` | `integer` |
| `Decimal` | `decimal`, `number` |
| `Date` | `date` |
| `DateTime` | `datetime`, `date-time` |
| `Boolean` | `boolean` |

### 4. Custom Type References
For references to other business objects:
- Use the exact business object name
- For arrays, append `[]`: `"type": "Address[]"`

---

## Complete Template

```json
{
  "name": "ExampleBusinessObject",
  "namespace": "YourContext",
  "description": "Brief description of the business object",
  "type": "businessObject",
  "properties": [
    {
      "name": "id",
      "type": "String",
      "required": true,
      "description": "Unique identifier"
    },
    {
      "name": "name",
      "type": "String",
      "required": true,
      "description": "Display name"
    },
    {
      "name": "amount",
      "type": "Decimal",
      "required": true,
      "description": "Monetary amount"
    },
    {
      "name": "quantity",
      "type": "Integer",
      "required": false,
      "description": "Item quantity"
    },
    {
      "name": "isActive",
      "type": "Boolean",
      "required": true,
      "description": "Active status flag"
    },
    {
      "name": "createdDate",
      "type": "DateTime",
      "required": true,
      "description": "Creation timestamp"
    },
    {
      "name": "effectiveDate",
      "type": "Date",
      "required": false,
      "description": "Effective date (date only, no time)"
    },
    {
      "name": "status",
      "type": "String",
      "required": true,
      "description": "Current status",
      "enum": ["Active", "Inactive", "Pending", "Closed"]
    },
    {
      "name": "relatedObject",
      "type": "OtherBusinessObject",
      "required": false,
      "description": "Reference to another business object"
    },
    {
      "name": "items",
      "type": "LineItem[]",
      "required": false,
      "description": "Array of line items"
    }
  ]
}
```

---

## Property Object Structure

Each property in the `properties` array must have:

### Required Fields
- **`name`** (string): Property name in camelCase
- **`type`** (string): BAW type name (see Type Names table above)
- **`required`** (boolean): Whether the property is mandatory
- **`description`** (string): Clear description of the property

### Optional Fields
- **`enum`** (array): List of allowed values for enumerated types
- **`minLength`** (integer): Minimum string length
- **`maxLength`** (integer): Maximum string length
- **`minimum`** (number): Minimum numeric value
- **`maximum`** (number): Maximum numeric value
- **`pattern`** (string): Regex pattern for validation
- **`default`** (any): Default value

---

## Examples by Type

### String Property
```json
{
  "name": "emailAddress",
  "type": "String",
  "required": true,
  "description": "Email address",
  "pattern": "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$"
}
```

### Enumerated String
```json
{
  "name": "status",
  "type": "String",
  "required": true,
  "description": "Payment status",
  "enum": ["Pending", "Approved", "Rejected", "Cancelled"]
}
```

### Decimal (Money)
```json
{
  "name": "amount",
  "type": "Decimal",
  "required": true,
  "description": "Transaction amount",
  "minimum": 0
}
```

### Integer
```json
{
  "name": "retryCount",
  "type": "Integer",
  "required": false,
  "description": "Number of retry attempts",
  "minimum": 0,
  "maximum": 5,
  "default": 0
}
```

### Boolean
```json
{
  "name": "isVerified",
  "type": "Boolean",
  "required": true,
  "description": "Whether the record has been verified",
  "default": false
}
```

### Date (Date Only)
```json
{
  "name": "birthDate",
  "type": "Date",
  "required": false,
  "description": "Date of birth (YYYY-MM-DD)"
}
```

### DateTime (Date and Time)
```json
{
  "name": "lastModified",
  "type": "DateTime",
  "required": true,
  "description": "Last modification timestamp (ISO 8601)"
}
```

### Reference to Another Business Object
```json
{
  "name": "customer",
  "type": "Customer",
  "required": true,
  "description": "Reference to Customer business object"
}
```

### Array of Business Objects
```json
{
  "name": "addresses",
  "type": "Address[]",
  "required": false,
  "description": "List of addresses"
}
```

### Array of Primitives
```json
{
  "name": "tags",
  "type": "String[]",
  "required": false,
  "description": "List of tags"
}
```

---

## Validation Checklist

Before generating business objects, verify:

- [ ] `"type": "businessObject"` is set
- [ ] `properties` is an **array**, not an object
- [ ] Each property has `name`, `type`, `required`, and `description`
- [ ] Type names use PascalCase (e.g., `String`, not `string`)
- [ ] Property names use camelCase
- [ ] Business object name uses PascalCase
- [ ] Namespace matches the context folder name
- [ ] All referenced business objects exist or will be created
- [ ] Enum values are provided for enumerated types

---

## Scanner Compatibility

The business object scanner ([`toolkit_packager/scanner/business_object_scanner.py`](../toolkit_packager/scanner/business_object_scanner.py)) expects:

1. **Line 81:** `if data.get("type") == "businessObject"`
   - Only files with `"type": "businessObject"` are recognized

2. **Line 23:** `self.properties = data.get("properties", [])`
   - Properties must be an array (list)

3. **Line 35-36:** `for prop in self.properties: prop_type = prop.get("type", "")`
   - Each property must be an object with a `get()` method

4. **Line 38:** Type checking against `["String", "Integer", "Decimal", "Date", "Boolean"]`
   - Primitive types must use these exact names

---

## Common Mistakes to Avoid

### ❌ Mistake 1: Wrong Type Field
```json
{
  "type": "complex"  // WRONG
}
```

### ❌ Mistake 2: Properties as Object
```json
{
  "properties": {  // WRONG - should be array
    "name": { "type": "string" }
  }
}
```

### ❌ Mistake 3: Lowercase Type Names
```json
{
  "name": "amount",
  "type": "decimal"  // WRONG - should be "Decimal"
}
```

### ❌ Mistake 4: Missing Required Fields
```json
{
  "name": "status",
  "type": "String"
  // MISSING: required, description
}
```

---

## Quick Reference

### Minimal Valid Business Object
```json
{
  "name": "MinimalExample",
  "namespace": "Context",
  "description": "Minimal valid business object",
  "type": "businessObject",
  "properties": [
    {
      "name": "id",
      "type": "String",
      "required": true,
      "description": "Identifier"
    }
  ]
}
```

### File Naming Convention
- Use PascalCase: `Customer.json`, `PaymentInstruction.json`
- Match the business object name: If `"name": "Customer"`, file should be `Customer.json`
- Place in context folder: `business-objects/generated/[Context]/[Name].json`

---

## Related Documentation

- [BAW Blueprint Parser Mode Rules](../.bob/rules-baw-blueprint-parser/1_workflow.xml)
- [Business Object Scanner](../toolkit_packager/scanner/business_object_scanner.py)
- [Business Object Generator](../toolkit_packager/generators/business_object_generator.py)
- [Custom Types Registry](../toolkit_packager/baw_custom_types.json)

---

**Last Updated:** 2026-06-18  
**Version:** 1.0.0