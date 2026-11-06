# Cigo MCP data handling and retention status

Updated: 2026-11-07. Operator: Cigo Co., Ltd. (씨고 주식회사).
Contact for access, correction, deletion and service questions: **cigo240920@gmail.com**.

## What is processed

Tool arguments are transmitted over HTTPS to Cigo's hosted server on Render.
Product lookups can record the supplied vehicle/filter query fields, channel label,
returned products, time and a journey identifier in Supabase. These records are not
the AI application's entire conversation. A channel label does not establish a
person's identity or the website where they first discovered Cigo.

The B2B inquiry tool stores the supplied company, contact name, email and optional
phone, country, language, subject, details, quantity and specifications in Supabase.
When translation is enabled, the subject and details are sent to Microsoft Azure
Translator for Korean translation. The original and translated inquiry are stored.
Configured Gmail notifications alert company staff to a submitted inquiry.

The replacement-date tool stores a hashed identifier, vehicle/driving information,
registration date and recommended replacement date in a server-side file. Hashing
does not make the whole record anonymous. This is not a scheduled reminder service.

The environment tool sends a supplied region/location query to the weather service.
Purchase preparation produces external store links; it does not create an account,
confirm an order or charge a payment. Store checkout has the store's own policies.
Do not provide passwords, payment information or unrelated personal information.

## Retention targets and current limitation

The operator has selected the following retention targets:

| Record | Selected retention target |
| --- | --- |
| Completed inquiry and its associated translation/handling details | 3 months after consultation is completed |
| Product lookup records | 3 months after collection |
| Uncompleted inquiry | 1 year after the last customer contact |
| Replacement-date record | 1 year after registration |

These are selected targets, **not a claim that automatic deletion currently runs**.
Scheduled purge enforcement, completion/last-contact tracking and handling of
infrastructure logs, backups and email copies have not yet been verified for these
targets. Records may remain until the operator processes deletion. This document
does not represent the outstanding implementation work as complete.

## Deletion requests and user choice

Email **cigo240920@gmail.com** with the inquiry number or other relevant record
reference and the requested correction/deletion. Do not send a password or identity
document. The operator will identify the relevant record and handle the request;
this connector does not offer automatic self-service deletion. Disconnecting the
AI app does not delete records already submitted to Cigo.

You may use product information without invoking the inquiry or replacement-date
tools; product usage logging can still occur. Before a write action, the client
must show the proposed information and ask for confirmation. Report successful
submission only after a successful server result.

## Connection and review limitations

The remote endpoint currently requires no API key and advertises both lookup and
write-capable tools. Client confirmation guidance is not an authentication control.
B2B validation checks required fields, email syntax, input lengths and language
codes. This is not a claim of a complete security audit or verified rate limiting.
Marketplace client-specific installation verification is tracked separately from
protocol-level initialize/tools/list checks.
