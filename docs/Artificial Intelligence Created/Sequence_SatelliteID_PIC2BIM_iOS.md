
# 🛰️ UML Sequence Diagram: `satelliteID` Processing in PIC2BIM iOS

This diagram represents the flow of data and actions related to handling the `satelliteID` within the PIC2BIM iOS application.

---

## 🧩 Mermaid Sequence Diagram

```mermaid
sequenceDiagram
    participant User
    participant GNSSModule
    participant GNSSReceiver
    participant NMEADecoder
    participant OSNMAValidator
    participant PhotoTagger

    User ->> GNSSModule: Start GNSS session
    GNSSModule ->> GNSSReceiver: Collect GNSS data
    GNSSReceiver ->> NMEADecoder: Parse satelliteID
    NMEADecoder ->> OSNMAValidator: Validate satelliteID authenticity
    OSNMAValidator -->> NMEADecoder: Authenticated/Unauthenticated
    OSNMAValidator ->> PhotoTagger: Send validated satelliteID
    PhotoTagger ->> User: Display tagged photo info
```

---

## ✅ Summary

- The `satelliteID` is captured and decoded from GNSS signals.
- OSNMA validation ensures the identity and integrity of the source satellite.
- The verified `satelliteID` is associated with captured photos for geospatial trust.
- This supports use cases requiring verifiable positioning data.

