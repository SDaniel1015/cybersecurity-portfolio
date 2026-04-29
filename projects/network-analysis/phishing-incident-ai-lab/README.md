├── README.md
# AI-Assisted Phishing Incident Analysis Lab

## Overview
This project demonstrates how AI can be used to assist in creating a cybersecurity incident report, along with the importance of human validation.

As a beginner in cybersecurity, I used AI to generate an initial phishing incident report, then reviewed and refined it to improve clarity and completeness.

## Objectives
- Use AI to generate a SOC-style phishing incident report
- Evaluate the accuracy and usefulness of AI-generated content
- Understand the role of human validation in cybersecurity workflows

## Files
- `prompt.txt` — The exact prompt used to generate the report
- `raw_ai_output.txt` — Initial AI-generated report
- `final_report.md` — Improved and structured version of the report
- `reflection.md` — Evaluation of AI effectiveness and limitations

## Key Takeaways
- AI is useful for generating structured starting points
- AI output may sound correct but still require validation
- Human oversight is necessary, especially in technical fields like cybersecurity

## Skills Demonstrated
- Basic incident analysis
- Understanding phishing attack structure
- AI-assisted workflow usage
- Critical thinking and evaluation

## Tools Used
- ChatGPT (AI generation)
- GitHub (project documentation)

## Future Improvements
- Improve ability to validate technical accuracy (MITRE ATT&CK, IOCs)
- Add real log analysis examples
- Expand into automated detection or scripting projects
├── prompt.txt
You are a cybersecurity analyst. Create a detailed phishing incident report based on a simulated attack.

Include:
- Executive summary
- Attack description
- Indicators of compromise (IPs, domains, email headers)
- MITRE ATT&CK techniques used
- Impact assessment
- Remediation steps
- User awareness recommendations

Format it as a professional SOC report.
├── raw_ai_output.txt
# Security Operations Center (SOC) Incident Report

## 1. Executive Summary

On March 28, 2026, a phishing email campaign targeted employees within the organization, attempting to harvest user credentials by impersonating a trusted service provider. Multiple users received an email prompting them to reset their passwords via a malicious link. One user interacted with the link and submitted their credentials.

The incident was detected by the security team through abnormal login activity and user reporting. Immediate containment actions were taken to prevent further compromise.

---

## 2. Attack Description

The attacker sent a phishing email disguised as a password reset notification from “IT Support.” The email contained urgent language encouraging users to reset their passwords within 24 hours to avoid account suspension.

The embedded link redirected users to a spoofed login page that closely resembled the organization’s legitimate authentication portal. The page captured user credentials and transmitted them to an external server controlled by the attacker.

After obtaining credentials, the attacker attempted to log in from an external IP address not previously associated with the user.

---

## 3. Indicators of Compromise (IOCs)

### Malicious Domains
- secure-login-alerts[.]com  
- account-verification-now[.]net  

### Suspicious IP Addresses
- 185.234.219.87  
- 45.77.112.54  

### Email Header Indicators
- From: IT Support <support@secure-login-alerts.com>  
- Reply-To: reset@account-verification-now.net  
- SPF: Fail  
- DKIM: None  
- DMARC: Fail  

### URL Observed
- http://secure-login-alerts.com/reset-password  

---

## 4. MITRE ATT&CK Techniques

- T1566.002 – Phishing: Spearphishing Link  
- T1078 – Valid Accounts  
- T1204 – User Execution  

---

## 5. Impact Assessment

- One user account was confirmed compromised.  
- Unauthorized login attempts were detected from a foreign IP address.  
- Potential access to internal systems and sensitive data.  
- No evidence of lateral movement at this time.  

---

## 6. Remediation Steps

- Disabled the compromised user account.  
- Forced password reset for affected users.  
- Blocked malicious domains and IP addresses at the firewall level.  
- Conducted endpoint scans for malware.  
- Reviewed authentication logs for suspicious activity.  

---

## 7. User Awareness Recommendations

- Educate users on identifying phishing emails.  
- Encourage verification of email sources before clicking links.  
- Promote reporting of suspicious emails to IT/security teams.  
- Reinforce the importance of strong, unique passwords.  
- Implement multi-factor authentication (MFA).  
├── final_report.md
# Security Operations Center (SOC) Incident Report

## 1. Executive Summary

On March 28, 2026, a phishing email campaign targeted employees within the organization, attempting to harvest user credentials by impersonating a trusted service provider. Multiple users received an email prompting them to reset their passwords via a malicious link, and one user successfully submitted credentials to a fraudulent login page.

The incident was detected through abnormal login activity and user reporting, triggering a security investigation and immediate containment response.

**Severity Level:** HIGH  
**Justification:** Credential compromise with confirmed unauthorized login attempts indicates a high likelihood of account misuse and potential access to sensitive systems.

---

## 2. Attack Description

The attacker sent a phishing email disguised as a password reset notification from “IT Support,” using spoofed branding and urgent language to create a sense of urgency. The email instructed users to reset their password within 24 hours to avoid account suspension.

The embedded link redirected users to a spoofed login page visually mimicking the organization’s authentication portal, including logo and layout replication. Upon credential submission, data was transmitted via an HTTP POST request to an attacker-controlled server.

After obtaining credentials, the attacker attempted to log in from an external IP address originating from a Russia-based ASN, which deviates from the user’s normal U.S.-based login activity.

---

## 3. Indicators of Compromise (IOCs)

### Malicious Domains
- secure-login-alerts[.]com  
- account-verification-now[.]net  

**Domain Registration Insight:** Recently registered (within 7 days), indicating likely attacker-controlled infrastructure.

### Suspicious IP Addresses
- 185.234.219.87  
- 45.77.112.54  

**Geolocation:** Eastern Europe (commonly associated with credential harvesting campaigns)

### Email Header Indicators
- From: IT Support <support@secure-login-alerts.com>  
- Reply-To: reset@account-verification-now.net  
- SPF: Fail  
- DKIM: None  
- DMARC: Fail  

**Observation:** Header authentication failures indicate a spoofed sender domain.

### URL Observed
- http://secure-login-alerts.com/reset-password  

**Additional Indicators:**
- No HTTPS encryption (no SSL certificate present)  
- URL does not match the organization’s official domain  

### Authentication Log Evidence
- Timestamp: 2026-03-28 14:32 UTC  
- User: j.doe@company.com  
- Source IP: 185.234.219.87  
- User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)  
- Login Status: SUCCESS (followed by anomaly detection alert)

---

## 4. MITRE ATT&CK Techniques

- T1566.002 – Phishing: Spearphishing Link  
- T1078 – Valid Accounts  
- T1204 – User Execution  
- T1056 – Input Capture (Credential Harvesting)  
- T1098 – Account Manipulation  

---

## 5. Impact Assessment

One user account was confirmed compromised. Unauthorized login attempts were detected from IP address 185.234.219.87, which is inconsistent with the user’s normal login behavior.

Potential risks include unauthorized access to internal systems, exposure of sensitive organizational data, and possible lateral movement if elevated privileges were obtained. At this time, there is no evidence of lateral movement, but monitoring remains ongoing.

**Business Impact:** Although limited to a single account, the incident represents a high-risk scenario due to credential compromise, which could lead to broader system access if not contained quickly.

---

## 6. Remediation Steps

The compromised user account was disabled immediately upon detection. Password resets were enforced for affected users, and all active sessions were terminated to prevent continued access.

Malicious domains and IP addresses were blocked at the firewall level. Conditional access policies were implemented to restrict logins from high-risk geographic locations.

Multi-factor authentication (MFA) was enforced for all users. Endpoint scans were conducted to ensure no malware was present, and authentication logs were reviewed for any additional suspicious activity.

Email filtering rules were updated to detect and block similar phishing attempts in the future.

---

## 7. User Awareness Recommendations

Users should be educated on how to identify phishing emails, including recognizing suspicious links, domain mismatches, and urgent or threatening language.

Employees should verify email sources before clicking on links and report any suspicious messages to the IT or security team immediately.

Simulated phishing exercises should be conducted regularly to improve awareness and response. Users should also be encouraged to use strong, unique passwords and rely on multi-factor authentication for additional account protection.

---

## 8. Timeline of Events

- 14:10 UTC – Phishing email delivered to multiple users  
- 14:32 UTC – User submitted credentials via malicious link  
- 14:35 UTC – Suspicious login detected from external IP  
- 14:37 UTC – Alert triggered in SIEM system  
- 14:45 UTC – Security team initiated response  
- 15:00 UTC – Account disabled and containment actions executed  
└── reflection.md
Describe the manual corrections you made. Why was human validation necessary in this scenario?

Since I’m still learning about SOC processes, I didn’t make a large number of deep technical corrections to the report. Most of my changes were focused on improving clarity, organization, and making sure the content made sense overall. For example, I added structure where needed, made certain sections easier to understand, and included additional context like a severity level and timeline to make the report feel more complete.

Human validation was still necessary because even though the AI output looked professional, I couldn’t fully trust that everything was accurate. There were areas where I wasn’t confident in the level of detail, especially in things like the MITRE ATT&CK mapping and indicators of compromise. This showed me that AI can generate something that sounds correct, but without enough knowledge, it’s hard to verify if it actually is.

Did using AI save you time compared to completing the task entirely from scratch?

Yes, using AI saved me a significant amount of time. If I had to create this report from scratch, I would have had to research what a phishing incident report should include, how to structure it, and what kind of technical details are expected. Since I’m still new to this, that would have taken much longer.

The AI gave me a strong starting point with everything already organized, which made the process more about reviewing and understanding the content instead of building it from nothing. I’d estimate it saved me around 50–60% of the time. At the same time, it also showed me that while AI is useful for getting started, I still need to build my own knowledge so I can properly evaluate and improve what it produces.
