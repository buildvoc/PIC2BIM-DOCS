
# 🔄 UML Sequence Diagram: OSNMAParser in PIC2BIM iOS

This sequence diagram outlines the flow of operations for parsing and validating OSNMA (Open Service Navigation Message Authentication) messages using the `OSNMAParser` component in the PIC2BIM iOS application.

---

## 🧩 UML Sequence Diagram

```plantuml
@startuml
  participant App
  participant GNSSReceiver
  participant OSNMAParser
  participant OSNMAValidator
  participant MetadataHandler

  App->>GNSSReceiver: Start GNSS Session
  GNSSReceiver->>OSNMAParser: Parse E1B Message
  OSNMAParser->>OSNMAValidator: Validate Signature
  OSNMAValidator-->>OSNMAParser: Validation Result
  OSNMAParser-->>GNSSReceiver: Validated Message
  GNSSReceiver->>MetadataHandler: Attach Location to Photo
  MetadataHandler-->>App: Update UI/Report
@enduml
```

---

## ✅ Summary

- The `App` initiates a GNSS session which leads to data capture by `GNSSReceiver`.
- `OSNMAParser` extracts message content from Galileo E1B signals.
- `OSNMAValidator` performs cryptographic checks to authenticate the messages.
- Upon validation, metadata is generated and passed to the UI and reporting layers.

