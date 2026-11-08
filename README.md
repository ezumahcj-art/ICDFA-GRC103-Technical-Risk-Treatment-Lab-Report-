1. Submission Overview & Directory Structure

This bundle contains the evidence artifacts, command log outputs, system configuration files, redacted log extracts, calculation workbook, and screenshots required for the Module 3 Technical Risk Treatment Lab submission.


Evidence ZIP Structure (submission_evidence.zip)

submission_evidence.zip
├── README.md                           # This mapping document
├── Technical_Risk_Treatment_Report.pdf  # Compiled PDF Milestone Report
├── outputs/                            # Raw command output text files
│   ├── baseline-time.txt               # Step 4: Baseline execution timestamp
│   ├── baseline-ports.txt              # Step 4: Baseline Nmap port scan
│   ├── baseline-web.txt                # Step 4: Baseline web server response
│   ├── baseline-listing.txt            # Step 4: Baseline directory listing
│   ├── baseline-file.txt               # Step 4: Baseline dummy file retrieval
│   ├── baseline-legacy.txt             # Step 4: Baseline legacy endpoint response
│   ├── avoidance-ports.txt             # Step 6: Avoidance post-treatment port scan
│   ├── avoidance-legacy.txt            # Step 6: Avoidance closed port response
│   ├── ufw-status.txt                  # Step 8: UFW firewall rule verification
│   ├── portal-before.sha256            # Step 10: Original portal file hash
│   ├── recovery-start.txt              # Step 10: Recovery exercise start timestamp
│   └── recovery-end.txt                # Step 10: Recovery exercise completion timestamp
├── configs/                            # Relevant configuration files
│   ├── nginx-grc-lab.conf              # Step 3 & 7: Nginx site configuration
│   └── grc-legacy.service              # Step 2: Systemd legacy service unit file
├── logs/                               # Redacted log extracts
│   ├── nginx_access_redacted.log       # Step 9: Redacted Nginx access log
│   └── ufw_redacted.log                # Step 9: Redacted UFW kernel firewall log
├── screenshots/                        # Corroborating lab screenshots
│   ├── 01-baseline-nmap.png            # Baseline open ports (80 & 8080)
│   ├── 02-avoidance-kali.png           # Avoidance validation (Port 8080 closed)
│   ├── 03-ufw-blocked-timeout.png      # UFW unapproved IP connection timeout
│   └── 04-hash-verification-success.png# SHA-256 hash restoration verification
└── calculation_workbook.xlsx           # Step 12: Cost analysis & Financial Risk Model


2. Evidence Mapping to Lab Steps

Lab Step	Step Title	Generated Evidence File(s)	Key Command / Evidence Description
Step 1	Prepare Ubuntu Environment	outputs/baseline-ports.txt	ip -br addr (IPs: Ubuntu 192.168.56.20, Kali 192.168.56.10)
Step 2	Create Content & Legacy Service	configs/grc-legacy.service	systemctl status grc-legacy listening on 0.0.0.0:8080
Step 3	Configure Lab Web Service	configs/nginx-grc-lab.conf	Nginx site block with autoindex on; custom log paths
Step 4	Collect Baseline Evidence	outputs/baseline-*.txt
screenshots/01-baseline-nmap.png	nmap -sT -p 80,8080 showing both ports open; HTTP 200 responses
Step 5	Baseline Risk Register	Technical_Risk_Treatment_Report.pdf (Section 3)	Risk scoring matrix (R1–R4) mapping assets, threats, and severity
Step 6	Apply Avoidance (Legacy Service)	outputs/avoidance-ports.txt
outputs/avoidance-legacy.txt	systemctl disable --now grc-legacy; Port 8080 verified closed
Step 7	Remove Archive Publication	configs/nginx-grc-lab.conf
Technical_Risk_Treatment_Report.pdf	Archive moved to /srv/grc-private/; Nginx HTTP 403 response
Step 8	Restrict Network via UFW	outputs/ufw-status.txt
screenshots/03-ufw-blocked-timeout.png	UFW default deny; source 192.168.56.11 times out after 5000ms
Step 9	Correlate Control Evidence	logs/nginx_access_redacted.log
logs/ufw_redacted.log	Evidence table matching HTTP 200/403 in Nginx and dropped SYN in UFW
Step 10	Backup & Recover Portal	outputs/portal-before.sha256
outputs/recovery-*.txt	File deletion, tar extraction, and sha256sum -c hash match in 2m 15s
Step 11	Model Transfer & Acceptance	Technical_Risk_Treatment_Report.pdf (Section 7)	Managed backup evaluation & 14-day temporary HTTP risk acceptance
Step 12	Compare Costs & Remaining Risk	calculation_workbook.xlsx
Technical_Risk_Treatment_Report.pdf	Options A+B analysis ($510 1st yr cost), ALE model ($440 net benefit)


3. Change, Rollback & Integrity Summary


Change Record (Step 6): Disable legacy Python endpoint (grc-legacy.service). Rollback command tested: sudo systemctl enable --now grc-legacy. Final state: Service disabled.

Firewall Rollback Record (Step 8): UFW test rule applied. Console rollback command verified: sudo ufw disable. Final state: UFW enabled with strict source allowlist.

Recovery Timing (Step 10): Total observed RTO = 2 minutes, 15 seconds. Hash verification returned OK with zero cryptographic drift.

Data Privacy Verification: Confirmed that no private keys, passwords, or VM disk images (.vdi, .vmdk, .qcow2) are present in this submission bundle.
