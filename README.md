# 🎫 IT Ticket Management System - n8n Workflows


A complete automated IT support ticket management system built with n8n that handles ticket creation, tracking, and status updates through form submissions and email integration.

---

## 🏗️ Overview

This project consists of two interconnected n8n workflows that automate the entire IT support ticket lifecycle, from initial ticket creation through resolution tracking and status updates.

---

## Workflows Included:

1.IT Ticket Management System - Handles new ticket creation and initial processing

2.Ticket Status Tracker - Monitors email responses and updates ticket status automatically

### ✨ Features

## 🎯 Core Functionality

- Automated Ticket Creation - From web form submissions.

- Unique Ticket ID Generation - Sequential numbering with custom prefixes.

- Real-time Email Notifications - Instant alerts to support team.

- Centralized Ticket Logging - Google Sheets integration for reporting.

- Automated Status Updates - Email-based ticket closure system.

- Priority Management - Support for Low, Medium, High priority levels.


## 🔧 Technical Features
- Missing values are filled:
  - Categorical: `'None'`
  - Numerical: `0`
- Categorical features are label-encoded using `LabelEncoder`.

### 3. 🛠️ Feature Engineering
- MySQL Integration - Reliable ticket counter management.

- Gmail Integration - Seamless email communication.

- Google Sheets API - Comprehensive audit trails.

- Custom JavaScript Logic - Flexible business rules.

- Scheduled Monitoring - Automated email checking.

- Conditional Processing - Smart ticket status detection.


### 🏗️ System Architecture
graph TB
    A[User Form Submission] --> B[Form Trigger]
    B --> C[MySQL Ticket Counter]
    C --> D[Generate Ticket ID]
    D --> E[Send Email Notification]
    E --> F[Google Sheets Logging]
    
    G[Scheduled Email Check] --> H[Gmail Monitoring]
    H --> I[Filter Support Responses]
    I --> J{Status Check}
    J -->|Completed| K[Update Ticket Status]
    J -->|Pending| H
    K --> F


### 📊 Workflow Details

# 1. IT Ticket Management System (IT Ticket Management System.json)
Purpose: Creates and processes new IT support tickets from form submissions.

Form Submission → MySQL Ticket Number Generation → Email Notification → Google Sheets Logging

Form Fields:
👤 Name (required) - Requester's full name

🏢 Department (required) - Department/team name

🐛 Issue Description (required) - Detailed problem description

⚡ Priority Level (required) - Low, Medium, High

Technical Components:
n8n-nodes-base.formTrigger - Web form handling

n8n-nodes-base.mySql - Database operations for ticket numbering

n8n-nodes-base.gmail - Email notifications to support team

n8n-nodes-base.googleSheets - Data logging and audit trail

n8n-nodes-base.code - Custom JavaScript for ticket ID generation

# 2. Ticket Status Tracker (Ticket_Status_Tracker.json)
Purpose: Monitors email responses and automatically updates ticket status.

Scheduled Email Check → Filter Support Responses → Update Ticket Status → Close Tickets

Email Filtering Criteria:
📧 Subject: Contains "Re: Norpetco IT Ticket Support System"

👨‍💼 Sender: Specific support personnel email

✅ Content: Contains completion keywords (Done/accomplished/solved)

Technical Components:
n8n-nodes-base.scheduleTrigger - Time-based execution (every minute)

n8n-nodes-base.gmail - Email monitoring and retrieval

n8n-nodes-base.if - Conditional filtering logic

n8n-nodes-base.googleSheets - Status updates in spreadsheet

n8n-nodes-base.splitInBatches - Batch processing for multiple emails


### 🚀 Installation

# Prerequisites
✅ n8n instance (self-hosted or n8n.cloud).

✅ MySQL database (version 5.7 or higher).

✅ Gmail/Google Workspace account.

✅ Google Sheets document.

✅ Proper OAuth2 credentials configured in n8n.


## Step 1: Database Setup

Create the required MySQL table:

```sql
CREATE TABLE ticket_counter (
    id INT PRIMARY KEY,
    current_number INT,
    ticket_prefix VARCHAR(50)
);

-- Insert initial data
INSERT INTO ticket_counter (id, current_number, ticket_prefix) 
VALUES (1, 0, 'TICKET');
```
