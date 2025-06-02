
# 🛰️ OSNMA-Enabled Satellite Signals for PIC2BIM iOS — Detailed Analysis

This document provides a comprehensive analysis of how OSNMA (Open Service Navigation Message Authentication) is used in the PIC2BIM iOS application to enable trusted GNSS-based geolocation.

---

## 🔍 Document Objective

The document aims to **outline the integration of OSNMA** into the **PIC2BIM iOS** application by:

- Identifying the relevant **Galileo signals and satellites** (PRNs).
- Explaining the **purpose and functionality** of OSNMA.
- Providing a **UK-specific context** for visibility and use.
- Describing its **technical integration** into PIC2BIM iOS.

---

## 🧩 Functional Analysis

### ✅ OSNMA Support in Galileo

- **Technology**: OSNMA is a **cryptographic authentication scheme** provided by the **Galileo GNSS**.
- **Signal**: OSNMA is **transmitted via Galileo E1B** on 1575.42 MHz.
- **Purpose**: Ensures the **authenticity of navigation messages**, protecting against spoofing.

---

## 🛰️ Satellite-Specific Usage

### 📋 PRNs Supporting OSNMA (in UK Context)

| PRN | Satellite | Notes |
|-----|-----------|-------|
| E11 | GSAT0101  | ✅ OSNMA Capable |
| E12 | GSAT0102  | ✅ OSNMA Capable |
| E19 | GSAT0103  | ✅ OSNMA Capable |
| E20 | GSAT0104  | ✅ OSNMA Capable |
| E24 | GSAT0201  | ✅ OSNMA Capable |
| E25 | GSAT0202  | ✅ OSNMA Capable |
| E26 | GSAT0203  | ✅ OSNMA Capable |
| E27 | GSAT0204  | ✅ OSNMA Capable |
| E30 | GSAT0205  | ✅ OSNMA Capable |
| E31 | GSAT0206  | ✅ OSNMA Capable |

> These satellites frequently appear above the horizon in the UK and are compatible with OSNMA. Visibility depends on constellation health, user location, and satellite geometry.

---

## 📱 Integration in PIC2BIM iOS

### App-Specific Workflow

1. **Signal Capture**: Receives E1B signals from the Galileo satellites.
2. **Message Parsing**: Extracts navigation and authentication content.
3. **Validation**: Verifies digital signatures via OSNMA protocol.
4. **Integration**:
   - Validated signals are logged.
   - OSNMA status is embedded in geotagged photo metadata.
   - Used for trusted location documentation.

---

## 🛡️ Security & Integrity Benefits

| Feature             | Description |
|---------------------|-------------|
| **Spoofing Detection** | Ensures authenticity of satellite signal |
| **Message Integrity**   | Confirms trust in positioning messages |
| **Data Confidence**     | Adds assurance in audits and regulatory reporting |

---

## 🌍 Use in the UK

- OSNMA-enabled satellites are frequently visible across the UK.
- Suitable for field use in infrastructure inspection, construction, and geospatial asset management.

> GNSS planning tools like GPSTest or GNSS View can validate current PRNs overhead.

---

## 📌 Summary

- **Signal Used**: Galileo E1B
- **Satellites**: PRNs E11–E31
- **App Role**: Enables trusted, secure geotagging in PIC2BIM iOS
- **Security Outcome**: Authentication of navigation messages using OSNMA ensures **data integrity** and **spoofing resistance** in critical GNSS applications.
