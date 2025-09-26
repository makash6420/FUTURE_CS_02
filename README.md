from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.lib import colors

# File path
file_path = "/mnt/data/Task2_Incident_Report.pdf"

# Create document
doc = SimpleDocTemplate(file_path, pagesize=A4)
styles = getSampleStyleSheet()
story = []

# Title
story.append(Paragraph("<b>Task 2 — Security Alert Monitoring & Incident Response</b>", styles['Title']))
story.append(Spacer(1, 12))

# Student Info
story.append(Paragraph("*Student:* Your Name Here", styles['Normal']))
story.append(Paragraph("*Date:* DD/MM/YYYY", styles['Normal']))
story.append(Spacer(1, 12))

# Summary
story.append(Paragraph("<b>1. Summary</b>", styles['Heading2']))
story.append(Paragraph("Uploaded Windows event logs into Splunk, created searches to detect brute force, SQL Injection attempts, and privilege escalation. Configured alerts and documented incidents with remediation steps.", styles['Normal']))
story.append(Spacer(1, 12))

# Environment & Data
story.append(Paragraph("<b>2. Environment & Data</b>", styles['Heading2']))
story.append(Paragraph("Tool: Splunk Enterprise (Free Trial)<br/>Index: security_logs<br/>Log Files: sample.evtx (converted to CSV), web_access.log<br/>Conversion: PowerShell Get-WinEvent -Path sample.evtx | Export-Csv sample.csv", styles['Normal']))
story.append(Spacer(1, 12))

# Objectives
story.append(Paragraph("<b>3. Objectives</b>", styles['Heading2']))
story.append(Paragraph("1. Ingest and parse logs into Splunk.<br/>2. Create searches for suspicious activities.<br/>3. Configure alerts.<br/>4. Document incidents and remediation.", styles['Normal']))
story.append(Spacer(1, 12))

# Findings Table
story.append(Paragraph("<b>4. Findings</b>", styles['Heading2']))
data = [
    ["Incident ID", "Time", "Type", "Severity", "Status"],
    ["INC-001", "2025-09-24 10:15:23", "Brute Force (SSH)", "Medium", "Open"],
    ["INC-002", "2025-09-24 10:22:01", "SQL Injection", "High", "Resolved"],
    ["INC-003", "2025-09-24 10:35:42", "New Admin Creation", "High", "Open"]
]
table = Table(data, colWidths=[80, 120, 150, 80, 80])
table.setStyle(TableStyle([
    ('BACKGROUND', (0, 0), (-1, 0), colors.grey),
    ('TEXTCOLOR', (0, 0), (-1, 0), colors.whitesmoke),
    ('ALIGN', (0, 0), (-1, -1), 'CENTER'),
    ('GRID', (0, 0), (-1, -1), 1, colors.black),
    ('BACKGROUND', (0, 1), (-1, -1), colors.beige),
]))
story.append(table)
story.append(Spacer(1, 12))

# Recommendations
story.append(Paragraph("<b>5. Recommendations</b>", styles['Heading2']))
story.append(Paragraph("1. Enforce MFA for all admin accounts.<br/>2. Implement WAF rules to stop SQL injection.<br/>3. Harden SSH (disable root login, fail2ban).<br/>4. Regular log ingestion and monitoring.<br/>5. Create runbook for SOC operations.", styles['Normal']))
story.append(Spacer(1, 12))

# Conclusion
story.append(Paragraph("<b>6. Conclusion</b>", styles['Heading2']))
story.append(Paragraph("Through this task, I learned how to use Splunk for log ingestion, alert creation, and incident response. I practiced analyzing security events, classifying incidents, and recommending remediation. This improved my knowledge of SOC operations and incident response workflow.", styles['Normal']))

# Build PDF
doc.build(story)

file_path
