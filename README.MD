Task 3 – Vulnerability Assessment Using OpenVAS

Objective

Conduct a vulnerability assessment on a target system using **OpenVAS** (Greenbone Vulnerability Manager) and document the findings.

---

Tools Used

- Kali Linux (as the host operating system)
- Greenbone Vulnerability Manager (OpenVAS)
- PostgreSQL for OpenVAS database backend
- Firefox (for accessing the Greenbone Security Assistant web UI)

---

Steps Followed

1. Installation & Setup
- Updated system and installed required dependencies.
- Installed OpenVAS (sudo apt install openvas).
- Ran initial setup using:
  sudo gvm-setup
Checked configuration with:
sudo gvm-check-setup
           
2. Fixing Feed Sync Issues
Resolved SCAP and CERT feed errors by using:
sudo greenbone-feed-sync --type SCAP
sudo greenbone-feed-sync --type CERT
           
3. Database & Service Issues
Addressed PostgreSQL collation mismatch.
Restarted database and services:
sudo systemctl start postgresql
sudo systemctl restart gvmd ospd-openvas gsad
           
4. Launching Web UI
Started GSAD manually:
sudo gsad --no-redirect \
  --listen=127.0.0.1 \
  --port=9392 \
  --ssl-private-key=/var/lib/gvm/private/CA/serverkey.pem \
  --ssl-certificate=/var/lib/gvm/CA/servercert.pem \
  --foreground --verbose
Accessed via https://127.0.0.1:9392

5. Performing Scan
Created target, credentials, and scan task.
Ran full scan against the target system.
Exported report as PDF.
