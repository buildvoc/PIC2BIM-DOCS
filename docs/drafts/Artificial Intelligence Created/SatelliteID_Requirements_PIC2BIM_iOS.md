
# 🛰️ SatelliteID Requirements in PIC2BIM iOS

This document outlines which satellite signals are necessary for extracting and validating `satelliteID` in the PIC2BIM iOS application.

---

## ✅ Required Satellite Signals

PIC2BIM iOS relies primarily on **Galileo GNSS** signals, specifically:

### 🛰️ Galileo E1B (Open Service - OS)
- The **E1B signal** contains the **Navigation Message Authentication (OSNMA)** data.
- `satelliteID` is derived from the ephemeris and OSNMA fields within the navigation message.
- Only satellites broadcasting E1B with OSNMA capability are used for secure authentication.

---

## 🔄 Signal Processing Flow

1. **GNSS Receiver** captures raw E1B signals.
2. **OSNMA Parser** extracts `satelliteID` from navigation messages.
3. **Authentication Validator** checks signature integrity tied to `satelliteID`.
4. **Validated satelliteID** is used in:
   - Metadata for photos
   - OSNMA logs
   - Reports

---

## 📌 Satellite System Compatibility

| GNSS System | Signal Used | OSNMA Compatible | Usage in PIC2BIM |
|-------------|-------------|------------------|------------------|
| Galileo     | E1B         | ✅ Yes            | ✅ Primary Source |
| GPS         | L1 C/A      | ❌ No             | ❌ Not used       |
| GLONASS     | L1          | ❌ No             | ❌ Not used       |
| BeiDou      | B1          | ❌ No             | ❌ Not used       |

---

## 🔒 Why Use Galileo E1B?

- **Authenticity**: Ensures signal has not been spoofed.
- **Trustable Positioning**: Enables secure geotagging of media.
- **Field Reliability**: Enhances GNSS credibility in critical field operations.

