# Requirements Document: Policy2People AI

## 1. Problem Statement

Millions of eligible Indian citizens fail to access government welfare schemes due to systemic information barriers:

- **Complexity**: Policies are written in dense legal language with nested conditions, exceptions, and cross-references
- **Fragmentation**: Scheme information is scattered across multiple government portals, PDFs, circulars, and notifications
- **Lack of Structure**: Most policy documents are unstructured (scanned PDFs, image-based documents, inconsistent formats)
- **Interpretation Difficulty**: Citizens cannot determine eligibility without expert knowledge of policy nuances
- **Dynamic Nature**: Schemes are frequently updated with amendments, making static information quickly outdated

Existing government portals use rule-based filtering systems that:
- Require users to manually select predefined checkboxes
- Cannot understand natural language queries
- Fail to handle conditional, nested, or context-dependent eligibility criteria
- Provide no explanation for eligibility decisions
- Cannot reason about partial matches or borderline cases

**The Core Challenge**: Policy eligibility is not a simple checklist. It involves semantic understanding, contextual reasoning, and interpretation of complex conditional logic that traditional rule-based systems cannot handle effectively.

## 2. Objectives

Policy2People AI aims to democratize access to government welfare schemes by:

1. **Simplifying Discovery**: Enable citizens to find relevant schemes using natural language descriptions of their situation
2. **Intelligent Reasoning**: Perform multi-factor semantic eligibility analysis using generative AI
3. **Transparency**: Provide explainable results showing why a citizen is eligible or ineligible
4. **Proactive Guidance**: Identify missing documents and predict rejection probability
5. **Accessibility**: Support multilingual interaction for diverse Indian populations
6. **Scalability**: Build a cloud-native solution that can handle millions of users
7. **Accuracy**: Deliver high-confidence recommendations with clear uncertainty indicators

## 3. Scope of the System

### In Scope

- Ingestion and processing of unstructured government scheme PDFs
- AI-powered extraction of eligibility criteria from policy documents
- Natural language query interface for citizens
- Semantic eligibility reasoning using Large Language Models
- Explainable eligibility decisions with confidence scores
- Document gap analysis and rejection probability prediction
- Multilingual output support (English, Hindi, and regional languages)
- AWS cloud deployment with security and scalability
- Web-based user interface for citizen interaction

### Out of Scope

- Direct application submission to government portals
- Payment processing or financial transactions
- Real-time integration with government databases
- Mobile native applications (web-responsive only)
- Historical tracking of scheme changes over time
- User authentication and personalized dashboards (for hackathon MVP)

## 4. User Personas

### Persona 1: Rural Farmer (Primary User)
- **Name**: Lakshmi, 32 years old
- **Location**: Rural Karnataka
- **Education**: 8th grade
- **Language**: Kannada (limited English)
- **Income**: ₹1.8 lakh per year
- **Technology Access**: Basic smartphone, intermittent internet
- **Pain Points**: 
  - Cannot understand English policy documents
  - Unaware of schemes she qualifies for
  - Previously rejected due to incomplete documentation
- **Goals**: Find agricultural subsidies, women empowerment schemes, and loan programs

### Persona 2: Urban Youth (Secondary User)
- **Name**: Arjun, 24 years old
- **Location**: Mumbai
- **Education**: Graduate, unemployed
- **Language**: English and Hindi
- **Income**: No current income
- **Technology Access**: Smartphone and laptop, good internet
- **Pain Points**:
  - Overwhelmed by number of schemes across websites
  - Unsure which schemes apply to his specific situation
  - Needs guidance on required documents
- **Goals**: Find skill development programs, employment schemes, and startup funding

### Persona 3: Senior Citizen (Tertiary User)
- **Name**: Ramesh Kumar, 68 years old
- **Location**: Semi-urban Uttar Pradesh
- **Education**: 12th grade
- **Language**: Hindi
- **Income**: ₹3 lakh per year (pension)
- **Technology Access**: Basic smartphone, needs assistance
- **Pain Points**:
  - Difficulty navigating complex government websites
  - Confusion about age-based eligibility criteria
  - Needs simple, clear explanations
- **Goals**: Find pension schemes, healthcare benefits, and senior citizen welfare programs

### Persona 4: NGO Worker (Support User)
- **Name**: Priya Sharma, 35 years old
- **Role**: Field worker at rural development NGO
- **Education**: Post-graduate in Social Work
- **Language**: English, Hindi, Tamil
- **Technology Access**: Laptop, good internet
- **Pain Points**:
  - Spends hours researching schemes for beneficiaries
  - Needs to explain eligibility to multiple people daily
  - Requires reliable, up-to-date information
- **Goals**: Quickly identify relevant schemes for diverse beneficiary profiles

## 5. Functional Requirements

### 5.1 Document Ingestion and Processing

**FR-1.1**: The system SHALL accept government scheme documents in PDF format (text-based and scanned images)

**FR-1.2**: The system SHALL use Amazon Textract to extract text from scanned/image-based PDFs

**FR-1.3**: The system SHALL identify and extract the following information from policy documents:
- Scheme name and description
- Eligibility criteria (age, income, gender, location, occupation, caste/category, etc.)
- Required documents
- Benefits provided
- Application process
- Validity period and deadlines

**FR-1.4**: The system SHALL handle multi-page documents and preserve document structure

**FR-1.5**: The system SHALL store extracted policy data in a structured format (JSON/database)

### 5.2 Natural Language Query Interface

**FR-2.1**: The system SHALL accept user queries in natural language describing their personal situation

**FR-2.2**: The system SHALL support queries containing multiple attributes (e.g., "I am a 28-year-old woman farmer from Karnataka earning 2 lakh per year")

**FR-2.3**: The system SHALL extract relevant user attributes from natural language input using LLM-based parsing

**FR-2.4**: The system SHALL handle incomplete or ambiguous user inputs and request clarification when necessary

**FR-2.5**: The system SHALL support conversational follow-up questions

### 5.3 Semantic Eligibility Reasoning

**FR-3.1**: The system SHALL use Amazon Bedrock (Claude or similar LLM) to perform semantic eligibility analysis

**FR-3.2**: The system SHALL match user attributes against scheme eligibility criteria using contextual reasoning

**FR-3.3**: The system SHALL handle complex conditional logic including:
- Nested conditions (e.g., "women farmers below poverty line in drought-affected districts")
- Range-based criteria (e.g., "age between 18-35" or "income below ₹3 lakh")
- Exclusionary conditions (e.g., "not applicable if already receiving Scheme X")
- Context-dependent rules (e.g., "priority given to first-time applicants")

**FR-3.4**: The system SHALL rank schemes by relevance and eligibility match strength

**FR-3.5**: The system SHALL identify partial matches where user meets some but not all criteria

### 5.4 Explainable Results

**FR-4.1**: For each scheme, the system SHALL provide:
- Eligibility status (Eligible / Not Eligible / Partially Eligible)
- Confidence score (0-100%)
- Detailed explanation of matched criteria
- Detailed explanation of unmatched criteria
- List of required documents
- Missing documents (if any)

**FR-4.2**: The system SHALL highlight which specific user attributes satisfied which eligibility conditions

**FR-4.3**: The system SHALL explain why a user is ineligible in clear, non-technical language

**FR-4.4**: The system SHALL provide actionable next steps (e.g., "You need to obtain an income certificate")

### 5.5 Document Gap Analysis

**FR-5.1**: The system SHALL identify required documents for each eligible scheme

**FR-5.2**: The system SHALL detect missing documents based on user-provided information

**FR-5.3**: The system SHALL provide guidance on how to obtain missing documents

**FR-5.4**: The system SHALL prioritize schemes based on document availability

### 5.6 Rejection Probability Prediction

**FR-6.1**: The system SHALL calculate rejection probability for borderline cases

**FR-6.2**: The system SHALL consider factors such as:
- Incomplete documentation
- Borderline income/age thresholds
- Ambiguous eligibility conditions
- Historical rejection patterns (if data available)

**FR-6.3**: The system SHALL display rejection risk as Low / Medium / High with explanation

### 5.7 Multilingual Support

**FR-7.1**: The system SHALL accept input queries in English and Hindi

**FR-7.2**: The system SHALL translate output results into user's preferred language using Amazon Translate

**FR-7.3**: The system SHALL support at least 5 Indian languages: English, Hindi, Tamil, Telugu, Kannada

**FR-7.4**: The system SHALL preserve technical terms and scheme names in original language

### 5.8 User Interface

**FR-8.1**: The system SHALL provide a web-based interface accessible via browser

**FR-8.2**: The interface SHALL be mobile-responsive for smartphone users

**FR-8.3**: The interface SHALL include:
- Text input box for natural language queries
- Results display with expandable scheme details
- Language selection dropdown
- Clear visual indicators for eligibility status

**FR-8.4**: The interface SHALL display results in a scannable format with visual hierarchy

## 6. Non-Functional Requirements

### 6.1 Usability

**NFR-1.1**: The system SHALL be usable by citizens with basic literacy (8th grade reading level)

**NFR-1.2**: The interface SHALL follow accessibility guidelines (WCAG 2.1 Level AA)

**NFR-1.3**: Query results SHALL be displayed within 10 seconds for 95% of requests

**NFR-1.4**: The system SHALL provide helpful error messages in user's language

### 6.2 Reliability

**NFR-2.1**: The system SHALL have 99% uptime during hackathon demonstration period

**NFR-2.2**: The system SHALL gracefully handle LLM API failures with fallback responses

**NFR-2.3**: The system SHALL log all errors for debugging and improvement

### 6.3 Maintainability

**NFR-3.1**: The system SHALL use modular architecture for easy component updates

**NFR-3.2**: Policy documents SHALL be updateable without code changes

**NFR-3.3**: The system SHALL maintain version control for policy data

### 6.4 Portability

**NFR-4.1**: The system SHALL be deployable on AWS cloud infrastructure

**NFR-4.2**: The system SHALL use containerization (Docker) for consistent deployment

## 7. AI-Specific Requirements

### 7.1 Model Selection

**AI-1.1**: The system SHALL use Amazon Bedrock with Claude 3 (or equivalent) for eligibility reasoning

**AI-1.2**: The system SHALL use Amazon Textract for document text extraction

**AI-1.3**: The system SHALL use Amazon Translate for multilingual support

**AI-1.4**: The system MAY use Amazon Comprehend for entity extraction from user queries

### 7.2 Prompt Engineering

**AI-2.1**: The system SHALL use structured prompts that include:
- Policy eligibility criteria
- User attributes
- Clear instructions for reasoning
- Output format specification

**AI-2.2**: The system SHALL implement few-shot learning examples in prompts for consistent output

**AI-2.3**: The system SHALL use chain-of-thought prompting for complex eligibility decisions

### 7.3 Context Management

**AI-3.1**: The system SHALL provide relevant policy context to the LLM without exceeding token limits

**AI-3.2**: The system SHALL implement retrieval-augmented generation (RAG) if policy corpus exceeds LLM context window

**AI-3.3**: The system SHALL use vector embeddings (Amazon Bedrock Embeddings) for semantic policy search

### 7.4 Output Validation

**AI-4.1**: The system SHALL validate LLM outputs for required fields (eligibility status, confidence score, explanation)

**AI-4.2**: The system SHALL detect and handle hallucinations or inconsistent responses

**AI-4.3**: The system SHALL implement confidence thresholds below which human review is recommended

## 8. Justification for Generative AI (Why Not Rule-Based)

### 8.1 Limitations of Rule-Based Systems

Traditional rule-based systems fail for government scheme eligibility because:

1. **Conditional Complexity**: Policies contain nested IF-THEN-ELSE logic that requires hundreds of hardcoded rules
   - Example: "Women farmers in drought-affected districts with income below ₹2 lakh AND not receiving any other agricultural subsidy"
   
2. **Semantic Understanding**: Eligibility criteria use natural language that requires interpretation
   - Example: "Preference given to first-time entrepreneurs" - what defines "first-time"?
   
3. **Context Dependency**: Same criteria may have different meanings in different schemes
   - Example: "BPL status" may be defined differently across state and central schemes
   
4. **Ambiguity Handling**: Policies often have implicit assumptions or unstated conditions
   - Example: "Residents of rural areas" - how is "rural" defined? Does it include semi-urban?
   
5. **Maintenance Burden**: Every policy update requires manual rule recoding by developers
   
6. **Partial Matches**: Rule-based systems return binary yes/no; they cannot reason about "close matches" or "borderline cases"

### 8.2 Advantages of Generative AI

Generative AI (LLMs) provide:

1. **Semantic Reasoning**: Understand natural language eligibility criteria without explicit rule encoding
2. **Contextual Interpretation**: Apply common sense and domain knowledge to ambiguous conditions
3. **Explainability**: Generate human-readable explanations for decisions
4. **Flexibility**: Adapt to new schemes without code changes - just provide policy text
5. **Nuanced Decisions**: Handle partial matches, confidence scores, and borderline cases
6. **Natural Interaction**: Accept user queries in conversational language without structured forms

**Computational Complexity Advantage**: Eligibility determination involves combinatorial reasoning across multiple dynamic attributes. As the number of attributes increases (age, income, gender, location, category, occupation, prior benefits), rule-based systems scale exponentially in complexity. Generative AI handles this complexity through contextual reasoning without exponential rule growth

### 8.3 Hybrid Approach

The system uses AI for reasoning but maintains structured data for:
- Fast retrieval of relevant schemes
- Validation of critical thresholds (age, income)
- Audit trails and compliance

## 9. Responsible AI Considerations

### 9.1 Bias and Fairness

**RAI-1.1**: The system SHALL NOT discriminate based on protected attributes (caste, religion, gender, disability)

**RAI-1.2**: The system SHALL be tested for bias across different demographic groups

**RAI-1.3**: The system SHALL provide equal quality of service regardless of user's language or location

**RAI-1.4**: The system SHALL monitor for systematic under-recommendation of schemes to specific groups

### 9.2 Transparency

**RAI-2.1**: The system SHALL clearly indicate that recommendations are AI-generated

**RAI-2.2**: The system SHALL provide confidence scores to indicate uncertainty

**RAI-2.3**: The system SHALL explain the basis for all eligibility decisions

**RAI-2.4**: The system SHALL NOT claim to provide legal advice or final eligibility determination

### 9.3 Data Privacy

**RAI-3.1**: The system SHALL NOT store personally identifiable information without consent

**RAI-3.2**: The system SHALL process user queries in-memory without persistent storage (for MVP)

**RAI-3.3**: The system SHALL comply with Indian data protection regulations

**RAI-3.4**: The system SHALL NOT share user data with third parties

### 9.4 Human Oversight

**RAI-4.1**: The system SHALL recommend human verification for low-confidence decisions

**RAI-4.2**: The system SHALL provide disclaimers that final eligibility is determined by government authorities

**RAI-4.3**: The system SHALL include feedback mechanism for incorrect recommendations

### 9.5 Accountability

**RAI-5.1**: The system SHALL log all AI decisions for audit purposes

**RAI-5.2**: The system SHALL maintain version control of AI models and prompts

**RAI-5.3**: The system SHALL provide contact information for reporting issues

## 10. Security Requirements

### 10.1 Data Security

**SEC-1.1**: The system SHALL encrypt data in transit using TLS 1.3

**SEC-1.2**: The system SHALL encrypt sensitive data at rest using AWS KMS

**SEC-1.3**: The system SHALL implement least-privilege access control for AWS resources

**SEC-1.4**: The system SHALL NOT log or store user personal information in plain text

### 10.2 API Security

**SEC-2.1**: The system SHALL implement rate limiting to prevent abuse

**SEC-2.2**: The system SHALL validate and sanitize all user inputs

**SEC-2.3**: The system SHALL protect against injection attacks (SQL, prompt injection)

**SEC-2.4**: The system SHALL use AWS IAM roles for service authentication

### 10.3 Infrastructure Security

**SEC-3.1**: The system SHALL deploy in AWS VPC with private subnets

**SEC-3.2**: The system SHALL use AWS WAF for web application firewall protection

**SEC-3.3**: The system SHALL implement CloudWatch monitoring and alerting

**SEC-3.4**: The system SHALL follow AWS Well-Architected Framework security pillar

## 11. Performance & Scalability Requirements

### 11.1 Performance

**PERF-1.1**: The system SHALL return eligibility results within 10 seconds for 95% of queries

**PERF-1.2**: The system SHALL process document ingestion within 2 minutes for 20-page PDFs

**PERF-1.3**: The system SHALL support concurrent queries with minimal latency degradation

**PERF-1.4**: The system SHALL cache frequently accessed policy data

### 11.2 Scalability

**SCALE-2.1**: The system SHALL handle at least 100 concurrent users during hackathon demo

**SCALE-2.2**: The system SHALL be architected to scale to 10,000+ concurrent users post-hackathon

**SCALE-2.3**: The system SHALL use serverless components (Lambda, API Gateway) for auto-scaling

**SCALE-2.4**: The system SHALL implement asynchronous processing for document ingestion

### 11.3 Cost Optimization

**COST-3.1**: The system SHALL minimize LLM API calls through intelligent caching

**COST-3.2**: The system SHALL use cost-effective AWS services for MVP (free tier where possible)

**COST-3.3**: The system SHALL implement request batching where applicable

## 12. Constraints and Assumptions

### 12.1 Constraints

**C-1**: Hackathon timeline: 24-48 hours for MVP development

**C-2**: Budget: Limited to AWS free tier or minimal spend (<$50)

**C-3**: Team size: 2-4 developers

**C-4**: No access to real-time government databases

**C-5**: Limited policy document corpus (10-20 schemes for demo)

**C-6**: No mobile app development (web-only)

### 12.2 Assumptions

**A-1**: Government scheme PDFs are publicly available and can be legally processed

**A-2**: AWS Bedrock access is available in the deployment region

**A-3**: Users have basic internet connectivity (3G or better)

**A-4**: Policy documents are in English or Hindi (primary languages)

**A-5**: Eligibility criteria in documents are sufficiently detailed for AI extraction

**A-6**: Users will provide truthful information about their situation

**A-7**: The system is a recommendation tool, not a legal authority

## 13. Success Metrics

### 13.1 Functional Success

**M-1**: Successfully ingest and process 10+ government scheme PDFs

**M-2**: Achieve 80%+ accuracy in eligibility determination (validated against known test cases)

**M-3**: Generate explainable results for 100% of queries

**M-4**: Support 3+ Indian languages for output

**M-5**: Provide confidence scores for all recommendations

### 13.2 User Experience Success

**M-6**: Average query response time < 10 seconds

**M-7**: User interface usable on mobile devices (responsive design)

**M-8**: Clear, understandable explanations (validated by user testing)

**M-9**: Zero critical security vulnerabilities

### 13.3 Technical Success

**M-10**: Successful deployment on AWS with 99% uptime during demo

**M-11**: Handle 50+ concurrent demo users without degradation

**M-12**: Modular architecture allowing easy addition of new schemes

**M-13**: Comprehensive logging and error handling

### 13.4 Hackathon Success

**M-14**: Clear demonstration of AI reasoning vs. rule-based approach

**M-15**: Compelling use case with real-world impact

**M-16**: Professional presentation with live demo

**M-17**: Well-documented code and architecture on GitHub

**M-18**: Demonstrate that at least 70% of test users discover at least one previously unknown scheme they are eligible for

## 14. Hackathon Alignment

### 14.1 Clarity

- **Problem**: Clearly defined - millions miss welfare benefits due to information barriers
- **Solution**: Specific - AI-powered semantic eligibility reasoning
- **Differentiation**: Explicit comparison with existing rule-based systems

### 14.2 Usability

- **Target Users**: Well-defined personas (rural farmers, urban youth, seniors, NGO workers)
- **Interface**: Simple natural language input, no complex forms
- **Accessibility**: Multilingual support, mobile-responsive, low literacy friendly

### 14.3 Public Impact

- **Scale**: Addresses problem affecting millions of Indian citizens
- **Equity**: Helps underserved populations access welfare benefits
- **Empowerment**: Provides transparency and understanding of eligibility
- **Measurable Benefit**: Increased scheme awareness and application success rates

### 14.4 Technical Innovation

- **AI Application**: Novel use of LLMs for policy reasoning
- **AWS Integration**: Comprehensive use of AWS AI services (Bedrock, Textract, Translate)
- **Explainability**: Transparent AI decision-making
- **Scalability**: Cloud-native architecture for real-world deployment

### 14.5 Feasibility

- **MVP Scope**: Achievable in hackathon timeframe
- **Technology Stack**: Proven AWS services
- **Demo-Ready**: Clear demonstration path with sample schemes
- **Extensibility**: Architecture supports post-hackathon enhancement

## 15. Differentiation: Not a Chatbot, But a Reasoning Engine

Policy2People AI is not a generic chatbot.

Unlike conversational bots that retrieve scheme descriptions, this system:

- **Parses unstructured policy documents**: Extracts eligibility logic from PDFs, not just text
- **Converts them into structured eligibility knowledge**: Creates machine-understandable policy representations
- **Performs multi-factor semantic reasoning**: Evaluates multiple attributes simultaneously with contextual understanding
- **Evaluates nested and conditional rules**: Handles complex IF-THEN-ELSE logic and cross-dependencies
- **Generates explainable eligibility logic**: Shows which conditions were matched and why
- **Predicts rejection probability**: Analyzes borderline cases and document gaps proactively

The AI performs analytical reasoning over policy conditions rather than simple question-answer retrieval.

This positions the system as a **Policy Reasoning Engine**, not a chatbot interface.

**Key Distinction**: A chatbot answers "What is Scheme X?" - Policy2People AI answers "Am I eligible for Scheme X and why?"

---

## Document Control

- Version: 1.0
- Created: 15-02-2026
- Status: Final – Hackathon Idea Submission
- Next Steps: Prototype development and validation




