
# 📸🛰️ UML Sequence Diagram: `OSNMAEnabled` with `CameraViewController` (PIC2BIM iOS)

This diagram illustrates the interaction between the `CameraViewController` and GNSS-related components responsible for handling OSNMA (Open Service Navigation Message Authentication) functionality in the PIC2BIM iOS application.

```mermaid
sequenceDiagram
    participant User
    participant CameraViewController
    participant GNSSManager
    participant OSNMAValidator
    participant MetadataHandler

    User ->> CameraViewController: Open camera screen
    CameraViewController ->> GNSSManager: Request current GNSS data
    GNSSManager ->> OSNMAValidator: Check satellite data for OSNMA
    OSNMAValidator -->> GNSSManager: Return validated satellite IDs
    GNSSManager -->> CameraViewController: Provide satellite IDs with OSNMA status
    CameraViewController ->> MetadataHandler: Attach OSNMA-enabled PRNs to photo metadata
    User ->> CameraViewController: Capture photo
    CameraViewController ->> MetadataHandler: Finalize metadata (timestamp, location, OSNMA)
    MetadataHandler -->> CameraViewController: Metadata ready
    CameraViewController -->> User: Confirm photo saved with trusted GNSS data
```

---

## 🔍 Summary

- `GNSSManager` collects GNSS data including Galileo E1B.
- `OSNMAValidator` processes navigation messages for cryptographic verification.
- `CameraViewController` uses this data to geotag photos securely.
- Only satellites validated by OSNMA are included in the metadata to enhance authenticity.

> 📌 This ensures that PIC2BIM iOS produces field data with verifiable location information backed by secure GNSS authentication.

