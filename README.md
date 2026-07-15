# Privacy Policy — Smart Health Monitor

**Last updated:** July 15, 2026

This Privacy Policy explains how Smart Health Monitor collects, uses, stores, and shares information when you use the App. Smart Health Monitor is a healthcare-monitoring app that connects patients, caretakers, and doctors, and integrates with a wearable/bedside ESP32 sensor device.

---

## 1. Who this applies to

The App has three account types: **Patient**, **Caretaker**, and **Doctor**. This policy applies to all three. Caretakers and doctors may view a linked patient's health data as part of the App's core caregiving function — see Section 4.

## 2. Information we collect

### 2.1 Account & profile information
When you create an account, we collect:
- Name, email address (used for sign-in via Firebase Authentication)
- Phone number (optional)
- Age, gender, weight, height (optional, used to personalize risk analysis)
- City, country (optional, self-reported — the App does not access GPS or device location)
- Medical condition notes (optional, patient-entered)
- For doctor accounts: specialization, medical license/registration number, affiliated hospital or clinic

### 2.2 Health data
- Vital sign readings: heart rate, systolic/diastolic blood pressure, oxygen saturation (SpO2), body temperature
- Readings streamed from a connected ESP32-based sensor device (heart rate, SpO2, finger-detection status, device ID, timestamp)
- Notes attached to individual readings
- ML-generated risk classification results (risk level, confidence score, recommendation) — see Section 3
- Medicine records: medicine name, dosage, schedule, and adherence logs (taken/missed doses)
- Prescriptions and doctor's clinical notes, including diagnosis and follow-up dates, where a doctor account is linked to a patient

### 2.3 Automatically collected information
- **Push notification token** (Firebase Cloud Messaging), used to deliver medicine reminders and critical-vitals alerts to the patient and their linked caretakers/doctors
- **Crash and error diagnostics** (Firebase Crashlytics), including device model, OS version, app version, and stack traces, collected only from release builds
- We do **not** collect precise or approximate device location, contacts, camera, or microphone data. The App does not request location permissions.

## 3. How we use your information

| Purpose | Data used |
|---|---|
| Provide the core monitoring service (dashboards, history, trends) | Health readings, profile data |
| Generate an automated risk classification for a reading | Blood pressure, heart rate, SpO2, age, height, weight — sent to our third-party ML prediction service (see Section 5) |
| Send medicine reminders and critical-vitals alerts | Push notification token, medicine schedule, alert thresholds |
| Let a caretaker or doctor monitor a linked patient | Health data, medicine logs, profile data — limited to accounts the patient has explicitly linked |
| Diagnose and fix app crashes | Crash/error diagnostics |
| Secure your account | Email/password via Firebase Authentication |

We do **not** use your health data for advertising, and we do **not** sell your data.

## 4. How data is shared between accounts

Health data is visible only to accounts you (the patient) have explicitly linked:
- A **caretaker** linked to a patient can see that patient's readings, medicine adherence, and alerts.
- A **doctor** linked to a patient can see that patient's readings and history, and can add clinical notes and prescriptions.

Linking is performed through the App's account-linking flow and enforced server-side (Firestore security rules and Cloud Functions) — a caretaker or doctor cannot see a patient's data without an established link.

## 5. Third-party services we use

| Service | Purpose | Data shared |
|---|---|---|
| Firebase Authentication (Google) | Account sign-in | Email, password (hashed by Firebase; we never see the plaintext) |
| Cloud Firestore (Google) | Storing profile, medicine, and prescription data | As described in Section 2 |
| Firebase Realtime Database (Google) | Streaming live sensor readings | Sensor readings, device ID |
| Firebase Cloud Messaging (Google) | Push notifications | Push token |
| Firebase Crashlytics (Google) | Crash/error reporting | Device diagnostics, stack traces |
| ML prediction service (hosted on Railway) | Automated risk classification of a submitted reading | Blood pressure, heart rate, SpO2, age, height, weight (that single reading only). The prediction service itself is stateless: it computes a result in memory and does not write the reading to any database or file, and its application logs record only the request metadata (method, status, latency, IP) and the resulting risk label — never the raw vitals. (Note: this describes our application code; the underlying hosting provider's own infrastructure-level access logs are governed by their standard terms, as with any cloud host.) |

We do not share your data with advertisers or data brokers.

## 6. Data retention and deletion

You can permanently delete your account and all associated data (profile, readings, medicine logs, prescriptions, notes) from within the App: **Settings → Account → Delete Account**. Deletion is immediate and cascades across all linked records tied to your account. This action cannot be undone.

## 7. Data security

Data in transit is encrypted (HTTPS/TLS). Access to your data is restricted by Firebase Authentication and server-enforced Firestore/Realtime Database security rules, so only your account and accounts you've explicitly linked can read your health data.

## 8. Children's privacy

Smart Health Monitor is not directed at children under 13 (or the minimum age defined by your local law), and we do not knowingly collect data from children.

## 9. Your rights

Depending on your location, you may have rights to access, correct, export, or delete your personal data. You can manage most of this directly in the App, or contact us using the details below.

## 10. Changes to this policy

We may update this policy from time to time. Material changes will be reflected by updating the "Last updated" date above.

## 11. Contact us

Smart Health Monitor is developed and maintained by:

- Abubakar Abbasi — bcs223049@cust.pk
- Shaheer Samad Waien — bcs223065@cust.pk
- Chaudhary Ahmed Waseem — bcs223211@cust.pk

For any privacy questions, data access/deletion requests, or concerns about how your information is handled, please reach out to any of the above.

---

*This document is a starting draft based on the data the App actually collects, not a substitute for legal advice. Consider having it reviewed by a lawyer, particularly regarding health-data regulations (e.g. HIPAA if you have US healthcare-provider customers, GDPR if you have EU/UK users) that may apply depending on where you launch and who your users are.*
