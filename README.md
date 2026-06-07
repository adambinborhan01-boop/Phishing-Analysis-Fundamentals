# Phishing Emails

A walkthrough of the TryHackMe **Phishing Emails** room covering email fundamentals, header analysis, attachment investigation, phishing detection, and basic email forensics.

## Room Information

| Category | Value |
|-----------|---------|
| Platform | TryHackMe |
| Room | Phishing Emails |
| Difficulty | Easy |
| Topics | Email Analysis, Phishing, Email Headers, Attachments, OSINT |

---

## Task 1 - Introduction

This room introduces the fundamentals of phishing analysis and explains how attackers abuse email infrastructure to deliver malicious content.

Topics covered:

- Email delivery basics
- Email header analysis
- Email body analysis
- Common phishing techniques
- Attachment investigation

---

## Task 2 - The Email Address

An email address consists of:

```text
username@domain
```

Example:

```text
hatsalesman@tryhatme.com
```

### Question

Identify the domain used in the following email address:

```text
hatsalesman@tryhatme.com
```

### Answer

```text
tryhatme.com
```

---

## Task 3 - Email Delivery

Email delivery relies on several protocols:

| Protocol | Purpose |
|-----------|----------|
| SMTP | Sends email |
| POP3 | Downloads email to a device |
| IMAP | Synchronizes email across devices |
| DNS | Locates the recipient's mail server |

### Questions

#### Which protocol is responsible for sending an email from a client to a mail server?

```text
SMTP
```

#### Which service is used to look up the recipient domain's mail server?

```text
DNS
```

#### Bob wants to access his email from multiple devices, including his phone and laptop. Which protocol should he use?

```text
IMAP
```

---

## Task 4 - Email Headers

Email headers provide valuable metadata about a message, including sender information, routing details, and authentication results.

### Investigating the Email Source

Open:

```text
Email Samples/email1.eml
```

View the raw source in Thunderbird:

```text
View -> Message Source
```

or

```text
Ctrl + U
```

### Evidence

![Email Header Analysis](thmphishingemails/email%20ip.png)

### Question

What is the full subject line of `email1.eml`?

### Answer

```text
Help protect your budget by protecting your home
```

### Question

What IP address is listed as the `X-Originating-IP`?

### Answer

```text
43.255.56.161
```

---

## Task 5 - Email Body

Email bodies may contain plain text, HTML content, embedded images, links, and attachments.

### Attachment Analysis

Open:

```text
Email Samples/email2.txt
```

Review the attachment metadata contained within the message source.

### Evidence

![Attachment Metadata](thmphishingemails/content%20type.png)

### Question

What is the `Content-Type` of the attachment?

### Answer

```text
application/pdf
```

### Question

What is the attachment filename?

### Answer

```text
zmqpalgh.pdf
```

---

### Attachment Reconstruction

The attachment is Base64 encoded within the email source.

After decoding the content and opening the reconstructed PDF, the hidden flag can be recovered.

### Evidence

![Decoded PDF](thmphishingemails/pdf%20decode.png)

### Question

What is the hidden flag value?

### Answer

```text
THM{BENIGN_PDF_ATTACHMENT}
```

---

## Task 6 - Types of Phishing

Common phishing categories include:

- Spam
- Phishing
- Spear Phishing
- Whaling
- Smishing
- Vishing

Indicators of phishing emails:

- Spoofed sender addresses
- Urgent language
- Brand impersonation
- Suspicious hyperlinks
- Malicious attachments

### Investigation

Analyze:

```text
Email Samples/email3.eml
```

### Evidence

![Home Depot Phishing Email](thmphishingemails/home%20depot.png)

### Question

Which reputable organization is being spoofed in this phishing attempt?

### Answer

```text
Home Depot
```

### Question

What is the sender's email address?

### Answer

```text
support@teckbe.com
```

### Question

What is the defanged `X-Originating-IP`?

### Answer

```text
103[.]234[.]236[.]83
```

### Question

Which mail server generated the `Authentication-Results` header?

### Answer

```text
atlas102.free.mail.gq1.yahoo.com
```

---

## Task 7 - Conclusion

Business Email Compromise (BEC) is a phishing technique where attackers gain access to or impersonate legitimate business email accounts to trick employees into performing fraudulent actions.

### Question

What attack, signified by the acronym BEC, uses a compromised email to trick employees into fraud?

### Answer

```text
Business Email Compromise
```

---

## Answers Summary

| Task | Answer |
|--------|---------|
| 2 | tryhatme.com |
| 3.1 | SMTP |
| 3.2 | DNS |
| 3.3 | IMAP |
| 4.1 | Help protect your budget by protecting your home |
| 4.2 | 43.255.56.161 |
| 5.1 | application/pdf |
| 5.2 | zmqpalgh.pdf |
| 5.3 | THM{BENIGN_PDF_ATTACHMENT} |
| 6.1 | Home Depot |
| 6.2 | support@teckbe.com |
| 6.3 | 103[.]234[.]236[.]83 |
| 6.4 | atlas102.free.mail.gq1.yahoo.com |
| 7 | Business Email Compromise |

---
