Policy2People AI 🇮🇳  
AI-Powered Government Scheme Eligibility Reasoning Engine  

Bridging the gap between complex public policies and Indian citizens through explainable Generative AI built on AWS.


The Problem

Millions of eligible Indian citizens miss out on government welfare schemes because policy information is complex, scattered, and difficult to interpret.

• Policies are written in dense legal language  
• Eligibility rules are multi-layered and conditional  
• Information is spread across multiple portals  
• Systems are static and rule-based  
• There is limited multilingual personalization  

Most platforms provide scheme descriptions — but not personalized eligibility reasoning.


Our Solution

Policy2People AI is a semantic policy reasoning engine that:

• Parses unstructured government scheme documents  
• Interprets eligibility criteria using Generative AI  
• Matches citizen profiles conversationally  
• Clearly explains why a user is eligible or not  
• Identifies missing documents  
• Provides multilingual responses  

This is not a chatbot.  
It is an AI-powered eligibility reasoning system designed for public impact.


How It Works

1. Government scheme PDFs are stored in Amazon S3  
2. Amazon Textract extracts text from policy documents  
3. Eligibility metadata is structured and stored in DynamoDB  
4. A citizen submits their profile or query  
5. AWS Lambda processes the request  
6. Amazon Bedrock performs semantic reasoning  
7. The system generates explainable results  
8. Amazon Translate converts output to the selected language (if required)  


Confidence Score Logic

Confidence is calculated based on how many eligibility conditions are satisfied and the strength of contextual match.

• 80–100% → High Confidence  
• 60–79% → Moderate Confidence  
• 40–59% → Low Confidence  
• Below 40% → Not Recommended  


Example Input and Output

Example 1 – Rural Farmer

Input:
"I am a 32-year-old woman farmer from Karnataka earning 1.8 lakh per year."

Output:

ELIGIBLE for PM-KISAN  
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


Example 2 – Urban Youth

Input:
"I am a 24-year-old graduate from Mumbai and currently unemployed."

Output:

ELIGIBLE for Skill Development Schemes  
Confidence Score: 84% (High)

PARTIALLY ELIGIBLE for Startup India  
Confidence Score: 61% (Moderate)

Missing Requirement:
• Business registration  

Alternative Suggestions:
• PMKVY  
• Stand-Up India  
• MUDRA Yojana  


AWS Architecture

The solution is designed using a serverless and scalable AWS architecture:

User → Amazon API Gateway → AWS Lambda →  
Amazon DynamoDB + Amazon S3 → Amazon Bedrock → Response  

Core AWS Services Used:

• Amazon Bedrock – Generative AI reasoning  
• Amazon Textract – Policy document text extraction  
• Amazon S3 – Secure document storage  
• Amazon DynamoDB – Structured eligibility metadata  
• AWS Lambda – Serverless backend logic  
• Amazon API Gateway – REST API interface  
• Amazon Translate – Multilingual support  
• AWS IAM – Access control  
• Amazon CloudWatch – Monitoring and logging  


Why AI Instead of Rules?

Government policies often contain:

• Nested eligibility conditions  
• Context-based interpretations  
• Conditional clauses  
• Exceptions and preferences  

Traditional systems rely on static filtering logic.  

Policy2People AI uses semantic reasoning via Large Language Models to interpret policy language contextually.

The system ensures explainability by showing:

• Which criteria were matched  
• Which were not matched  
• Confidence score  
• Risk indication  


Responsible AI Approach

Bias Mitigation  
The system avoids discrimination based on gender, caste, religion, or region.

Transparency  
Every recommendation includes reasoning and confidence scoring.

Privacy  
No long-term storage of sensitive personal data.  
Minimal data retention principles are followed.


Scalability and Security

• Fully serverless AWS architecture  
• Auto-scaling managed services  
• Encrypted storage in S3 and DynamoDB  
• IAM-based least privilege access  
• HTTPS endpoints via API Gateway  


Expected Impact

• Improved welfare scheme accessibility  
• Reduced rejection due to confusion  
• Multilingual inclusion for Bharat-scale reach  
• Reduced reliance on intermediaries  
• Increased policy transparency  


Current Status

This repository contains the conceptual architecture, AI workflow design, and documentation prepared for the AI for Bharat Hackathon.

The system is designed for deployment using a secure and scalable AWS cloud-native architecture.


Team

AI Bharath CloudForge

Shabarriesh Arjarapu – Team Lead  
K Pavan Kumar – AWS Architecture & Backend  
Punitha Rani – AI & Documentation  
B Kushwanth Sai – Frontend & System Design  
