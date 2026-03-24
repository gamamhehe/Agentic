---
name: Domain Project Instructions
description: Short project-specific domain reference for the Guidance Archive domain, focused on models, relationships, enums, and core business rules.
---

# Domain Project Instructions

> ⚠️ This file is project-specific and is the one exception in this template. Replace or remove it when reusing this guidance in another project.


## Related Pattern Files

- `patterns/CodePatterns.md`

## Purpose

This file describes the **project-specific domain model** for Guidance Archive.

Use it as a quick reference for:

- main business models
- model relationships
- enums

Use together with:

- `instructions/Domain.instructions.md` = general domain design principles

---

# Core Domain

The Guidance Archive domain is centered around **Document**.

`Document` is the main business entity in the system.  
It represents one guidance item in the archive, including metadata, source information, publication state, and relationships to other concepts.

Supporting reference models:

- `Organization`
- `DocumentType`
- `RelatedSystem`
- `Publisher`
- `Tag`

---

# Main Aggregate Root

## Document

`Document` is the main aggregate root.

It represents a guidance record, not only a file.  
A document may come from:

- an uploaded file
- an external website link

This is controlled by `SourceType`.

---

# Enums

## DocumentStatus

| Value | Meaning |
|---|---|
| `Draft` | Document is not yet published. |
| `Published` | Document is published and available. |

## SourceType

| Value | Meaning |
|---|---|
| `Document` | Source is an uploaded file. |
| `Website` | Source is an external URL. |

## AnalyzeStatus

| Value | Meaning |
|---|---|
| `Processing` | Document has been submitted to the Document Archive and is being analysed. |
| `Succeeded` | Document Archive analysis completed successfully. |
| `Failed` | Document Archive analysis failed. |

---

# Domain Models

## 1. Document

### Business meaning

Represents one guidance item in the archive.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Title` | `string` | Main title |
| `Status` | `DocumentStatus` | Draft or Published |
| `SourceType` | `SourceType` | Document or Website |
| `ExpireDate` | `DateTimeOffset?` | Optional expiration date |
| `OrganizationId` | `Guid` | Responsible organization |
| `OriginalReportLink` | `string?` | Original external link |
| `FileSize` | `long?` | File size in bytes; populated for `Document` source type |
| `ShortDescription` | `string?` | Short searchable summary; populated by Document Archive on success |
| `LongDescription` | `string?` | Long searchable summary; populated by Document Archive on success |
| `AnalyzeStatus` | `AnalyzeStatus?` | Tracks the Document Archive analysis lifecycle; null until first DA call |
| `CreatedAt` | `DateTimeOffset` | Created timestamp |
| `UpdatedAt` | `DateTimeOffset` | Updated timestamp |
| `CreatedBy` | `Guid` | User who created the record |
| `UpdatedBy` | `Guid` | User who last updated the record |
| `IsDeleted` | `bool` | The record is soft delete |

### Relationships

- one `Organization`
- many `DocumentType`
- many `Publishers`
- many `Tags`
- many `RelatedSystems`
- many `RelatedDocuments`

---

## 2. Organization

### Business meaning

Represents the Organization responsible for the document.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Name` | `string` | Organization name |
| `Cvr` | `string?` | Optional business code |
| `IsDeleted` | `bool` | The record is soft delete |


---

## 3. DocumentType

### Business meaning

Represents the classification of a document.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Name` | `string` | Type name |
| `IsDeleted` | `bool` | The record is soft delete |

---

## 4. RelatedSystem

### Business meaning

Represents a system associated with a document.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Name` | `string` | System name |
| `IsDeleted` | `bool` | The record is soft delete |


---

## 5. Publisher

### Business meaning

Represents a publisher or publishing party linked to a document.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Name` | `string` | Publisher name |
| `Cvr` | `string?` | Optional publisher CVR |
| `Email` | `string?` | Optional contact email |
| `IsDeleted` | `bool` | The record is soft delete |

---

## 6. Tag

### Business meaning

Represents a flexible label for filtering and search.

### Main properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Internal identifier |
| `Name` | `string` | Tag name |
| `IsDeleted` | `bool` | The record is soft delete |

---

# Related Documents

A document can reference other documents in the archive.

---

# Relationships

| From | To | Cardinality |
|---|---|---|
| `Document` | `Organization` | many-to-one |
| `Document` | `DocumentType` | many-to-many |
| `Document` | `Publisher` | many-to-many |
| `Document` | `Tag` | many-to-many |
| `Document` | `RelatedSystem` | many-to-many |
| `Document` | `Document` | self-reference |
