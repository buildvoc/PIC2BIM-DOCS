
# 🔐 UML Class Diagram: PublicKey in PIC2BIM iOS

This class diagram illustrates how the `PublicKey` functionality might be structured and interact with other components for OSNMA in the PIC2BIM iOS app.

---

## 🧩 Mermaid Class Diagram

```mermaid
classDiagram
  class PublicKeyManager {
    +loadKey()
    +verifySignature(data, signature)
    +getKeyId()
  }

  class OSNMAValidator {
    +validate(data)
    -parseSignatureBlock()
    PublicKeyManager keyManager
  }

  class GNSSMessage {
    +getE1BData()
    +getNavigationMessage()
  }

  GNSSMessage --> OSNMAValidator : provides data
  OSNMAValidator --> PublicKeyManager : uses for signature check
```

---

## ✅ Summary

- **PublicKeyManager**: Handles key management and signature verification for OSNMA.
- **OSNMAValidator**: Uses the public key to validate GNSS navigation messages.
- **GNSSMessage**: Supplies raw satellite message data to the validator.

This modular design supports secure, validated location data handling in offline or online modes.

