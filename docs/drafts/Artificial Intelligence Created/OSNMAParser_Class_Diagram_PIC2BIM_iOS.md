
# 📘 UML Class Diagram: `OSNMAParser` in PIC2BIM iOS

This class diagram represents the structure and relationships of the `OSNMAParser` component assumed to be responsible for parsing Open Service Navigation Message Authentication (OSNMA) data in the PIC2BIM iOS app.

---

## 🧩 Mermaid Class Diagram

```mermaid
classDiagram
    class OSNMAParser {
        +parse(message: GNSSMessage): OSNMAData
        +validateSignature(data: OSNMAData): Bool
        +extractKeys(): [PublicKey]
        -rawMessage: GNSSMessage
        -validationStatus: Bool
    }

    class GNSSMessage {
        +timestamp: Date
        +satelliteID: String
        +payload: Data
    }

    class OSNMAData {
        +signature: Data
        +authFlag: Bool
        +satelliteID: String
        +timestamp: Date
    }

    class PublicKey {
        +id: String
        +key: String
    }

    OSNMAParser --> GNSSMessage
    OSNMAParser --> OSNMAData
    OSNMAParser --> PublicKey
```

---

## ✅ Summary

- **OSNMAParser** acts as the main parser and validator for GNSS messages using OSNMA.
- It relies on `GNSSMessage` as input and generates `OSNMAData` for validation.
- **PublicKey** entities are used for signature verification.
- This modular design supports maintainable and secure authentication workflows in the app.

