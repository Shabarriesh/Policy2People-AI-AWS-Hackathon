# Policy2People AI 🇮🇳  
## AI-Powered Government Scheme Eligibility Reasoning Engine

Bridging the gap between complex public policies and Indian citizens through explainable Generative AI built on AWS.


---

## The Problem

Millions of eligible Indian citizens miss out on government welfare schemes because policy information is complex, scattered, and difficult to interpret.

• Policies are written in dense legal language  
• Eligibility rules are multi-layered and conditional  
• Information is spread across multiple portals  
• Systems are static and rule-based  
• Limited multilingual personalization  

Most platforms provide scheme descriptions — but not personalized eligibility reasoning.


---

## Our Solution

Policy2People AI is a semantic policy reasoning engine that:

• Parses unstructured government scheme documents  
• Interprets eligibility criteria using Generative AI  
• Matches citizen profiles conversationally  
• Clearly explains why a user is eligible or not  
• Identifies missing documents  
• Provides multilingual responses  

This is not just a chatbot.  
It is an AI-powered eligibility reasoning system designed for public impact.


---

## How It Works

1. Government scheme PDFs are stored in Amazon S3  
2. Amazon Textract extracts structured text  
3. Eligibility metadata is stored in DynamoDB  
4. A citizen submits their profile or query  
5. AWS Lambda processes the request  
6. Amazon Bedrock performs semantic reasoning  
7. The system generates explainable results  
8. Amazon Translate returns output in the chosen language  


---

## Confidence Score Logic

Confidence is calculated based on how many eligibility conditions are satisfied and the clarity of match.

• 90–100% → High Confidence  
• 70–89% → Medium Confidence  
• Below 70% → Low Confidence  

Confidence adjusts based on:

• Matched vs unmatched criteria  
• Missing critical information  
• Borderline threshold values  
• Ambiguous policy wording  


---

## Example Input and Output

### Example 1 – Rural Farmer

**Input:**  
"I am a 32-year-old woman farmer from Karnataka earning 1.8 lakh per year."

**Output:**

Eligible for PM-KISAN  
Confidence Score: 92% (High)

Matched Criteria:
• Age within eligible range  
• Occupation: Farmer  
• Income below threshold  
• Location valid  

Required Documents:
• Aadhaar Card  
• Land ownership proof  
• Bank account details  

Rejection Risk: Low


---

### Example 2 – Urban Youth

**Input:**  
"I am a 24-year-old graduate from Mumbai and currently unemployed."

**Output:**

Eligible for Skill Development Schemes  
Confidence Score: 84% (High)

Partially Eligible for Startup India  
Confidence Score: 61% (Medium)

Missing Requirement:
• Business registration  

Alternative Suggestions:
• PMKVY  
• Stand-Up India  
• MUDRA Yojana  


---

## AWS Architecture

The solution uses a serverless, scalable AWS architecture:

User → Amazon API Gateway → AWS Lambda →  
Amazon DynamoDB + Amazon S3 → Amazon Bedrock → Response  

Core AWS Services:

• Amazon Bedrock – Generative AI reasoning  
• Amazon Textract – Policy extraction  
• Amazon S3 – Document storage  
• Amazon DynamoDB – Eligibility metadata  
• AWS Lambda – Serverless backend  
• Amazon API Gateway – REST API interface  
• Amazon Translate – Multilingual output  
• AWS IAM – Access control  
• Amazon CloudWatch – Monitoring  


---

## Why AI Instead of Hardcoded Rules?

Government policies contain:

• Nested eligibility conditions  
• Context-based interpretations  
• Conditional clauses  
• Exceptions and preference rules  

Traditional rule systems grow exponentially in complexity.

Policy2People AI uses semantic reasoning through LLMs to interpret policy text contextually instead of relying on rigid rule trees.

The system provides:

• Matched criteria  
• Unmatched criteria  
• Clear explanations  
• Confidence scores  


---

## Responsible AI Approach

### Bias Mitigation
Designed to avoid discrimination based on gender, caste, religion, or region.

### Transparency
Every recommendation includes explanation and confidence scoring.

### Privacy
No long-term storage of sensitive personal data.  
Minimal data retention principles are followed.


---

## Scalability and Security

• Fully serverless AWS architecture  
• Auto-scaling managed services  
• Encrypted storage in S3 and DynamoDB  
• IAM-based least privilege access  
• HTTPS endpoints via API Gateway  


---

## Expected Impact

• Improves scheme awareness and accessibility  
• Reduces incorrect or rejected applications  
• Enables multilingual inclusion at Bharat scale  
• Reduces dependency on intermediaries  
• Increases transparency in welfare access  


---

## Current Status

This repository contains the conceptual architecture and documentation prepared for the AI for Bharat Hackathon.

The system is designed for deployment using a secure, scalable AWS cloud-native architecture.


---

## Team

### AI Bharath CloudForge

Shabarriesh Arjarapu – Team Lead  
K Pavan Kumar – AWS Architecture & Backend  
Punitha Rani – AI & Documentation  
B Kushwanth Sai – Frontend & System Design  
