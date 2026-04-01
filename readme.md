# Sentinel: Autonomous Activity & Security Pipeline 

Sentinel is an automated monitoring engine designed to perform real-time heuristic analysis on communication and development metadata. By integrating **Gmail** and **GitHub REST APIs** into a unified **n8n** workflow, the system identifies anomalies and potential security risks based on activity volume and time-series patterns.

##  System Architecture

The workflow follows a robust **Data Pipeline** design:
1. **Ingestion Layer:** Concurrent data fetching from Gmail (OAuth2) and GitHub (Personal Access Token) to minimize latency.
2. **Aggregation Layer:** Normalization of diverse JSON payloads into a structured buffer.
3. **Heuristic Engine:** A custom **JavaScript (V8)** node that evaluates incoming data against pre-defined security rules.
4. **Scoring Logic:** Calculation of a weighted **Anomaly Score** to determine the system's current threat level.



##  Technical Specifications

* **Automation Platform:** [n8n](https://n8n.io/)
* **Runtime Environment:** Node.js / V8 JavaScript Engine
* **Integration Protocols:** OAuth2, REST API, Webhooks
* **Timezone Synchronization:** Adjusted for UTC+3 (TR) to monitor off-hour (00:00 - 06:00) activities.

## Heuristic Analysis Logic

The core logic focuses on three primary security vectors:
* **Off-Hour Monitoring:** Detects repository events or high email traffic during sensitive night hours.
* **Traffic Volumetrics:** Identifies sudden spikes in incoming messages (potential phishing or spam bursts).
* **Activity Correlation:** Cross-references development events with communication frequency to build a comprehensive risk profile.

| Risk Level | Threshold | Action |
| :--- | :--- | :--- |
| **SAFE** | Score < 40 | System stable, no anomaly detected. |
| **CAUTION** | Score 40-79 | Moderate activity spike detected. |
| **DANGER** | Score ≥ 80 | Critical off-hour activity or volume burst. |



##  Deployment & Configuration

1.  **Workflow Import:** Import the provided JSON export into a local or cloud n8n instance.
2.  **API Credentials:** Configure Google Cloud Console for Gmail API and GitHub Developer Settings for repository access.
3.  **Variable Tuning:** Adjust the `anomalyScore` weights within the JavaScript node to fit specific security requirements.
<img width="1492" height="638" alt="image" src="https://github.com/user-attachments/assets/2838eeff-b9c8-41d5-bc73-69d1cf84cbb5" />


---
*This project is developed as a technical demonstration of API orchestration, data normalization, and autonomous monitoring logic.*
