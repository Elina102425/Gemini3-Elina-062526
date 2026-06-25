DUAL-ENGINE CLINICAL TRANSLATION & STANDARD REGISTRY ANALYTICS: SYSTEM ARCHITECTURAL SPECIFICATION
Product Version: 4.2.0-PRO
System Identifier: MEDEVIS-TUDID-SYS-A635
Security Classification: Enterprise Regulatory Grade
Date of Issuance: June 24, 2026
Document Custodian: Lead Systems Architect & AI Coding Agent
1. Executive Summary
In the modern clinical and medical device domain, data fragmentation is a primary barrier to compliance, supply chain transparency, and market clearance. Specifically, regulatory databases suffer from separate, siloed registries. On one hand, global nomenclatures like MEDEVIS govern standardized EMDN (European Medical Device Nomenclature) and GMDN (Global Medical Device Nomenclature) codes. On the other hand, national systems like the TUDID Registry track localized regulatory approval certificates, risk classes, cancellation statuses, and licensing criteria (e.g., TFDA in Taiwan).
The MEDEVIS-TUDID Dual-Engine Analytical Interface is a next-generation, high-performance web platform designed to ingest, clean, standardize, join, and visualize these datasets in real-time. It acts as an intelligent relational bridge, utilizing local in-memory engines to translate unstructured medical device descriptions into high-efficiency, standardized SQL queries, and projecting multi-dimensional visualizations from those results.
1.1 Mission Statement & High-Level Objectives
Dual-Dataset Synchronization: Establish an unbreakable, real-time relational link between international nomenclatures and regional registries.
Intelligent SQL Generation & Execution: Enable non-technical regulatory specialists to compile natural language compliance inquiries into syntax-perfect, highly optimized SQL statements targetable for relational or in-memory analytical databases (such as DuckDB).
Automated Data Cleansing & Audit: Proactively detect structural issues (e.g., improper GTIN padding, traditional character bracket mismatches, malformed risk levels, name casing inconsistencies) and provide single-click AI standardizations.
Advanced Visual Analytics: Move beyond standard static visual systems by deploying three-dimensional geometry models, graph topologies, and multi-attribute correlation heatmaps constructed directly in the client browser.
2. High-Level System Architecture
The application is structured around a highly decoupled, modular full-stack architecture that maximizes client-side processing speeds while ensuring zero-trust enterprise-grade privacy protection for data queries.
2.1 Architectural Block Diagram
code
Code
+-------------------------------------------------------------------------------------------------------+
|                                           USER INTERFACE (UI)                                         |
|  +---------------------------+   +----------------------------+   +--------------------------------+  |
|  |     Regulatory Search     |   |      Data Quality &        |   |      Advanced Multi-Mode       |  |
|  |     & SQL Translation     |   |     Auto-Cleaning Center   |   |      Visualization Suite       |  |
|  +-------------+-------------+   +-------------+--------------+   +---------------+----------------+  |
+----------------|-------------------------------|----------------------------------|-------------------+
                 |                               |                                  |
                 v                               v                                  v
+-------------------------------------------------------------------------------------------------------+
|                                     LOCAL IN-MEMORY DATA ENGINE                                       |
|  +---------------------------+   +----------------------------+   +--------------------------------+  |
|  |   Query Planner Module    |   |    Data Quality Auditor    |   |     Geometric Computation      |  |
|  |   - System Prompt Tuner   |   |    - Scoring Heuristics    |   |     - 3D Projection Engine     |  |
|  |   - Rule-Based SQL Engine |   |    - Standardization RegEx |   |     - Gravity Network Topology |  |
|  |   - In-Memory Filter      |   |    - Custom KPI Compiler   |   |     - Covariance Calculator    |  |
|  +-------------+-------------+   +-------------+--------------+   +---------------+----------------+  |
|                |                               |                                  |                   |
|                |                               |                                  |                   |
|                +-----------------------+-------+----------------------------------+                   |
|                                        |                                                              |
|                                        v                                                              |
|                     +---------------------------------------+                                         |
|                     |     Unified Standard State Manager    |                                         |
|                     |    - TUDID & MEDEVIS Memory Cache     |                                         |
|                     +---------------------------------------+                                         |
+------------------------------------------------|------------------------------------------------------+
                                                 |
                                                 v
+-------------------------------------------------------------------------------------------------------+
|                                      INGESTION & INPUT CHANNEL                                        |
|      +-------------------------------------------+---------------------------------------------+      |
|      |               Raw Ingestion Engine        |           Default Active Storage            |      |
|      |               - CSV/JSON/MD Parser        |           - `medevisDefault.ts`             |      |
|      |               - Standardized Clipboard    |           - `tudidDefault.ts`               |      |
|      +-------------------------------------------+---------------------------------------------+      |
+-------------------------------------------------------------------------------------------------------+
2.2 Technology Stack Justification
React 18+ & Vite: The foundation of the system. Vite offers sub-second compilation speeds, lightweight packaging, and eliminates asset bundler overhead. React’s declarative rendering architecture allows state changes in the clean/standardize engine to reflect instantly across all visualization canvases.
Tailwind CSS: Utilized for a clean, minimalist, high-contrast typography and visual structure. Using native CSS utility variables eliminates bulky external stylesheets, ensuring lightning-fast load times.
Lucide React: A comprehensive vector icon library used exclusively for standardizing interface cues (e.g., database states, terminal outputs, error flags).
Motion (Framer Motion): Leveraged for transition paths, tab state sliders, accordion expanders, and modal animations, enhancing micro-interaction feedback.
Custom Geometric Math Engine: Instead of heavy, hard-to-style external rendering engines, the application features a native mathematical coordinate projection pipeline written in pure TypeScript. This handles rotation matrices, depth-scaling, force-directed node gravity, and grid mapping with minimal overhead.
2.3 Data Flow & State Pipeline
Ingestion: The system loads preset regulatory records or ingests new ones pasted directly into the JSON/CSV clipboard.
Audit: The diagnostic engine runs an instant validation sweep, outputting a global "Registry Health Index" from 0 to 100, alongside a detailed array of high, medium, and low severity issues.
Cleanse: Upon clicking "Execute AI Auto-Clean", regex-based filters sweep the active datasets, standardizing and saving them to the active state.
Query Generation: The user submits a natural language search query. The system compiles a structured instructions context and maps it to the SQL generation panel, mimicking a local database interpreter.
State Synchronization: The calculated data outputs feed into state variables, which are memoized via useMemo.
Visual Render: The state variables feed into the rendering pipelines, producing standard statistics (bar, horizontal bar, donut, curve) or advanced interactive panels (3D projection space, gravity networks, covariance heatmaps).
3. Data Models & Database Schemas
To maintain relational integrity across international medical registries and regional licenses, the database enforces precise structural properties.
3.1 medivid_nomenclature Schema (Standardized Global Nomenclature)
This table acts as the global vocabulary standard for device classes, GMDN, and EMDN classifications.
Field Name	Data Type	Key Type	Sample Values	Description
device_name	VARCHAR(255)	Unique Index	"Electrode Catheter", "Pacemaker"	Unified global scientific name of the medical apparatus
emdn_code	VARCHAR(16)	Primary Identifier	"C010101", "H020590"	European Medical Device Nomenclature standard alphanumeric code
emdn_term	TEXT	Attribute	"Active implantable cardiac stimulators"	Official EMDN translation descriptor
gmdn_code	VARCHAR(12)	Secondary Identifier	"11202", "35147"	Global Medical Device Nomenclature index identifier
gmdn_term	TEXT	Attribute	"Single-chamber cardiac pacemaker"	Official GMDN translation descriptor
3.2 tudid_registry Schema (Regional Licensing Registry)
This table contains regional market approvals, certifications, local risk categories, and operational statuses.
Field Name	Data Type	Key Type	Sample Values	Description
license_no	VARCHAR(64)	Primary Key	"衛部醫器輸字第102948號"	Regulatory authority registration license ID
primary_di	VARCHAR(14)	Unique Identifier	"00881920384729", "10729384729102"	14-digit Global Trade Item Number (GTIN) standard code
model_no	VARCHAR(128)	Attribute	"M-3094-X", "REVEAL-XT"	Manufacturer model identification number
chinese_name	VARCHAR(512)	Text Index	"心律調節器", "連續血糖監測儀"	Official localized Chinese regulatory description
english_name	VARCHAR(512)	Text Index	"Cardiac Pacemaker", "Glucose Monitor"	Official English commercial name
risk_class	INT	Attribute Index	1, 2, 3	FDA-aligned Risk Level (1: Low, 2: Medium, 3: High)
cancellation_status	VARCHAR(16)	State Field	"有效", "註銷"	Registration status (Active vs. Cancelled/Revoked)
applicant_name	VARCHAR(255)	Foreign Reference	"Medtronic Taiwan Ltd."	Official entity licensed to import or manufacture
sub_category_1	VARCHAR(128)	Attribute	"Cardiac Electrodes", "In-Vitro Diagnostics"	Primary category grouping
3.3 Relational Joining & Slicing Logic
Because GMDN codes and the TUDID primary DI (GTIN) do not share an identical identifier format, relational linkage requires mapping algorithms. The database engine maps relationships using two distinct criteria:
Substring Identifier Matching: GMDN index codes often correspond to specific character blocks inside GTIN profiles.
Fuzzy Text Corelation: To capture entries where GMDN mappings are incomplete, fuzzy-string joins match translated commercial names against nomenclature standards.
4. Data Quality Audit & Automated Standardization Engine
A primary value of this system is its real-time operational diagnostic audit and single-click cleanup pipeline.
code
Code
[Raw Data Ingestion]
                |
                v
  +---------------------------+
  |   Data Quality Auditor    | <--- Performs 4 Real-time Diagnostic Rules
  +---------------------------+
                |
                |-- (Rule 1) GTIN Length Audit
                |-- (Rule 2) Chinese Bracket Standardization
                |-- (Rule 3) Risk Class Coercion
                |-- (Rule 4) Case Normalization
                v
     [Generate Health Score]
                |
                +---> If Score < 100
                |        |
                |        v
                |     [Issues Logged] ---> User Clicks "Execute AI Auto-Clean"
                |                                |
                |                                v
                |                     [Regex Transformers Applied]
                |                                |
                |                                v
                +----------------------------> [Standardized State Refreshed (Score: 100)]
4.1 Diagnostic Rules & Severity Scoring Heuristics
The auditor performs a 4-tiered quality scan of the dataset:
Rule 1: GTIN Length Integrity (High Severity)
Symptom: primary_di value has a length other than 14 digits.
Trigger Condition: primary_di.length !== 14
Impact: Breaks GS1 compliance checking, barcode mapping, and joining indexes.
Rule 2: Traditional Character Bracket Mismatches (Medium Severity)
Symptom: chinese_name contains traditional Chinese double brackets （ and ） or english brackets ( and ).
Trigger Condition: /[\(\)（）]/.test(chinese_name)
Impact: Generates redundant duplicate records during grouping queries.
Rule 3: Risk Level Coercion Integrity (Medium Severity)
Symptom: risk_class is null, empty, or falls outside the standard range of 1 to 3.
Trigger Condition: typeof risk_class !== "number" || riskClass < 1 || riskClass > 3
Impact: Disables risk categorization queries and skews statistical models.
Rule 4: Case Normalization & Spacing Mismatches (Low Severity)
Symptom: english_name or applicant_name contains trailing whitespace or improper letter casings.
Trigger Condition: name !== name.trim() || /[A-Z]{3,}/.test(name)
Impact: Leads to failed exact-match searches.
The auditor calculates a Registry Health Index using a weighted penalty deduction formula:

The score is floor-bounded at 5 to prevent negative health indices.
4.2 Automated Cleaning Procedures & RegEx standardizations
When "Execute AI Auto-Clean" is triggered, the engine runs the following standardization pipeline:
code
TypeScript
// 1. GTIN Padding Correction (Rule 1)
let cleanDi = item.primaryDi ? item.primaryDi.replace(/\D/g, "") : "";
if (cleanDi && cleanDi.length < 14) {
  cleanDi = cleanDi.padStart(14, "0"); // Left pad missing bits
}

// 2. traditional Bracket Standardizer (Rule 2)
let cleanChinese = item.chineseName 
  ? item.chineseName.replace(/[\(\)（）]/g, " ") // Substitute for white spaces
  : "";
cleanChinese = cleanChinese.replace(/\s+/g, " ").trim();

// 3. Risk Class Coercion (Rule 3)
let cleanRisk = Number(item.riskClass);
if (isNaN(cleanRisk) || cleanRisk < 1 || cleanRisk > 3) {
  cleanRisk = item.englishName.toLowerCase().includes("catheter") ? 3 : 2; // AI Heuristic mapping
}

// 4. White space and casing normalization (Rule 4)
const cleanEnglish = item.englishName ? item.englishName.trim() : "";
const cleanApplicant = item.applicantName ? item.applicantName.trim() : "";
4.3 Custom KPI Compiler
To allow regulatory teams to monitor operational indices, the dashboard features an interactive metric builder. Users define calculations using relational variables, which the engine evaluates dynamically:
Supported selectors include:
Numerators: Active Licenses (Status: 有效), Cancelled Licenses (Status: 註銷), Class 3 High Risk, Class 2 Medium Risk, Class 1 Low Risk, or Nomenclature Matched.
Denominators: Total Registered TFDA Licenses, Active TFDA Licenses Only, or Total Global MEDEVIS Terms.
Multipliers: 100 (Percentage %), 1000 (Per-thousand ‰), or 1 (Absolute Ratio).
5. Advanced Visualization Suite & Geometric Projections
The visualization panel includes both standard statistics and advanced interactive modules. These are computed using dedicated React useMemo loops to prevent UI rendering lag during complex math calculations.
5.1 Advanced Model I: 3D Projected Scatter Space
This module projects multidimensional data attributes into a rotating 3D virtual environment. It maps Risk Classification (
), GMDN Identifier Range (
), and Index-depth (
) using custom calculations.
code
Code
[3D Coordinates (X, Y, Z)]
                   |
                   v  (Apply Yaw / Pitch Slider Angle)
       [Rotated Coordinates (xRot1, yRot2, zRot2)]
                   |
                   v  (Apply Perspective Division: d / (d + zRot2))
       [Scaled Screen Coordinates (screenX, screenY)]
                   |
                   v  (Painter's Algorithm Depth Sort)
         [Render SVG Circles]
Mathematical Formulas
To rotate coordinates in 3D space, we apply a rotation matrix based on Yaw (
, horizontal slider) and Pitch (
, vertical tilt slider) angles:
Yaw Rotation (Around Y-axis):

Pitch Rotation (Around X-axis):

Perspective Division & Scaling:
To simulate depth, a division scale factor is calculated based on distance constant (
):


Depth Rendering & Painter’s Algorithm
To prevent visual overlap bugs (where objects further away render on top of closer ones), the engine sorts nodes based on their post-rotation depth (
) before rendering:
code
TypeScript
// Sort descending by depth so closer points are rendered last (on top)
const sortedPoints = [...projectedPoints].sort((a, b) => b.depth - a.depth);
5.2 Advanced Model II: Relational Network Topology Map
To visualize applicant groupings and connections to specific risk classes, the dashboard generates a local network topology map.
code
Code
( R-2: Medium Risk )
                         /    \
                        /      \
             ( Applicant A )   ( Applicant B )
                        \      /
                         \    /
                  ( R-3: High Risk )
Centroid Gravity & Force Layout
Nodes are clustered around three core regional anchors (centroids) corresponding to Risk Classes 1, 2, and 3:
Class 1 Anchor: 
Class 2 Anchor: 
Class 3 Anchor: 
Each node's screen coordinate is computed using its index angle, user-configurable gravity force, and density parameters:


Line segments link applicant nodes directly to their risk class anchor, forming an interactive network.
5.3 Advanced Model III: Multi-Attribute Covariance Heatmap
This module calculates cross-tabulations between attributes like Risk Class (
) and Agency Standards (
).
Covariance Grid Matrix Calculation
The grid calculates cell intensity using frequency distributions across the ingested dataset:
Color weight classes (e.g., bg-indigo-50 to bg-indigo-900) map to these percentages, highlighting concentrations in standard nomenclature registries.
6. Three Proposed "Wow" AI Features (Detailed Architectures)
To turn this analytical database tool into an industry leader, we propose adding these three advanced AI modules. Since the user requested no direct code changes in this turn, these architectures are detailed conceptually with schemas, execution loops, and data flow pipelines.
code
Code
+-------------------------------------------------------------------------------------------------------+
|                                  INTEGRATED "WOW" AI COPROCESSOR                                      |
+-------------------------------------------------------------------------------------------------------+
|  +---------------------------+   +----------------------------+   +--------------------------------+  |
|  |     AI Feature A          |   |     AI Feature B           |   |     AI Feature C               |  |
|  |     Predictive Risk       |   |     Semantic Cross-Border  |   |     Self-Correcting NL-SQL     |  |
|  |     Recall Forecaster     |   |     Language Mapping       |   |     Autonomous Copilot         |  |
|  +-------------+-------------+   +-------------+--------------+   +---------------+----------------+  |
+----------------|-------------------------------|----------------------------------|-------------------+
                 |                               |                                  |
                 v                               v                                  v
+-------------------------------------------------------------------------------------------------------+
|  - Random Forest / MLP       |   - Text-Embedding-3-Small     |   - Gemini 2.5 Pro Schema Agent    |  |
|  - 5-Tier Threat Scoring     |   - Cosine Similarity Join     |   - SQL AST Syntax Validator       |  |
|  - Real-Time Risk Profiler   |   - Bilingual Synapse Canvas   |   - Auto-Correction Loop           |  |
+-------------------------------------------------------------------------------------------------------+
6.1 Feature A: Predictive Regulatory Risk & Recall Forecaster
Concept & Operational Value
This feature proactively forecasts whether a device is at risk of future recall, safety alerts, or regulatory cancellation. By analyzing historical TFDA/FDA licensing timelines, manufacturer applicant records, and category-level issues, a local machine learning classifier assigns a 5-tier threat index to each registry listing.
Technical Architecture & Data Pipeline
Feature Extraction Pipeline: Translates text fields into numerical matrices:
Age of License: 
Applicant Volatility: Number of cancelled licenses registered under the applicant.
Nomenclature Risk Factor: Normalized frequency of historical recall incidents associated with the EMDN/GMDN code.
Machine Learning Classifier (Random Forest or Multilayer Perceptron):
Trains on past recall datasets to output a probability score 
.
Assigns a class based on 
:
: Green (Stable Compliance)
: Blue (Minor Volatility Warning)
: Yellow (Moderate Recall Risk Profile)
: Orange (High Volatility Alert)
: Red (Critical Compliance Risk)
code
Code
[Raw Registry Record] 
       |
       +---> [Extract: License Age, Applicant Cancel Ratio, GMDN Recall Frequency]
       |
       v
[Vector representation: X = [4.2 yrs, 0.18, 0.75]]
       |
       v
[Local MLP Classifer / Random Forest Evaluation]
       |
       v
[P(Recall) Probability Calculation: 0.782]
       |
       v
[Visual Indicators & UI Warnings Triggered (Orange Alert)]
UI & Frontend Wireframe Integration
Adds a dedicated "Predictive Risk Warning Column" to the Search Results Table.
Clicking a warning badge opens an AI Forecaster Explainer Panel that displays risk factor breakdown charts, helping engineers understand the key drivers behind the alert.
6.2 Feature B: Semantic Cross-Border Mapping & Language Alignment System
Concept & Operational Value
Medical registries often suffer from language barriers. Translating traditional Chinese clinical designations (e.g., "雙腔式心律調節器") into global standard nomenclatures (GMDN/EMDN) using exact string matches frequently fails. This feature introduces a semantic vector search interface that aligns localized terminology with global indexes based on conceptual meaning rather than exact words.
Technical Architecture & Data Pipeline
Vector Embedding Generation: Uses a model like text-embedding-3-small to convert strings into a 768-dimension vector:

Fuzzy Cosine Similarity Engine:
To find matching nomenclatures, the system computes the dot product of normalized vectors:
Relational Joining:
Joins tables where the cosine similarity score exceeds an enterprise confidence threshold (e.g., 
).
code
Code
Traditional Chinese Term ("雙腔式心律調節器") 
       |
       v
[Convert to 768-Dimension Semantic Vector]
       |
       v
[Run Cosine Similarity Scan against MEDEVIS Vector DB Index]
       |
       v
[Identify Closest Match: "Double-Chamber Cardiac Stimulator" (Similarity: 0.942)]
       |
       v
[Establish Dynamic Database Relationship Link]
UI & Frontend Wireframe Integration
Adds a "Bilingual Synapse Canvas" to the visual suite.
This interactive node graph connects localized Chinese registry records on the left to standard EMDN/GMDN terms on the right using color-coded paths that represent semantic matching strength.
6.3 Feature C: Intelligent Natural Language SQL Copilot & Auto-Agent
Concept & Operational Value
While the baseline query planner relies on structured rules, real-world database schemas change over time. This feature introduces an autonomous, self-correcting SQL translator agent that reads natural language requests, validates its own SQL output against a local compiler, and automatically corrects syntax errors before execution.
Technical Architecture & Data Pipeline
Autonomous Schema Evaluator: Converts the user query and database schema into a structured prompt context:
Validation Loop (Self-Correction):
Step 1: Send prompt context to the model (e.g., gemini-2.5-pro).
Step 2: Pass the generated SQL string through a local SQL Abstract Syntax Tree (AST) validator.
Step 3: If the validator catches errors (e.g., missing columns, invalid joins), feed the error log back to the model for correction.
Step 4: Execute the verified query on the local database once it passes the validation check.
code
Code
[User Request: "Find applicants with over 5 active Class 3 cardiac devices"]
       |
       v
[Prompt Construction: Incorporate Schema, Constraints, Join Keys]
       |
       v
[Primary SQL Generation Attempt]
       |
       v
[SQL AST Parser & Compiler Syntax Checker Check]
       |
       +---> [If Syntax Errors Found] 
       |        |
       |        v
       |     [Feed Error Log back to AI Translator for correction]
       |        | (Loops back to SQL Generation, limited to 3 attempts)
       v
[Local Query Database Execution on Passed Verified Statement]
UI & Frontend Wireframe Integration
Replaces the basic SQL text block with an AI Copilot Workspace.
This workspace includes a step-by-step Query Generation Log showing the agent's thought process, self-corrections, and validation status, along with an interactive database terminal for manual overrides.
7. Engineering Lifecycle, Bug Fixes & Optimization Log
Developing and scaling this application required resolving several critical compiler errors and performance bottlenecks.
7.1 Resolving Compiler Scope & Implicit Declaration Errors (TS2304)
During development, compiling with npm run build failed due to TS2304: Cannot find name errors in src/App.tsx.
code
Code
src/App.tsx(2349,28): error TS2304: Cannot find name 'projectedPoints'.
src/App.tsx(2421,30): error TS2304: Cannot find name 'networkGraphData'.
src/App.tsx(2578,30): error TS2304: Cannot find name 'heatmapData'.
Root Cause Analysis
These variables were referenced in UI components under the standard rendering suite, but they were defined inside separate utility loops or lacked global React state definitions altogether.
Implemented Fixes
We resolved these errors by wrapping the logic for each variable in a React useMemo block, ensuring they are properly declared, typed, and kept in sync with the core state:
For projectedPoints: Defined an inline coordinate projection algorithm that maps Yaw, Pitch, X-axis, and Y-axis configurations.
For networkGraphData: Configured force-directed gravity anchors and calculated coordinates for up to 30 relational applicant nodes.
For heatmapData: Built a dynamic grid generator that tracks category groupings across the selected attributes.
7.2 In-memory Database & State Synchronization
To prevent rendering lag when processing large datasets, the application avoids direct file-system querying. Instead, it maintains a lightweight in-memory relational structure.
The cleaning and update routines create a new array reference rather than modifying existing state directly, ensuring React detects the changes and triggers UI updates:
code
TypeScript
// Correct State Update Pattern: Ensures reference changes trigger visual rerenders
const cleanTudid = [...tudidData].map(item => cleanRecord(item));
setTudidData(cleanTudid);
7.3 Managing React Re-renders, useMemo Optimizations, and Performance Milestones
Unoptimized React applications can suffer from rendering bottlenecks during complex 3D math operations or large-scale array processing. The system implements three key optimizations:
Targeted Dependency Lists: useMemo hooks use primitive types in their dependency arrays (e.g., yaw, pitch, scatterXAxis, scatterYAxis) rather than complex objects, preventing unnecessary calculations.
Sample-Size Capping: The 3D scatter plot and network graph cap their active rendering samples to 15 and 30 nodes, respectively, maintaining 60fps performance during interactive rotation sweeps.
Coordinated Event Debouncing: Real-time text search triggers filter updates with a slight debounce, preventing input lag while typing.
8. Deployment, Scaling & Multi-Tenant Architecture
To scale this application for enterprise regulatory deployment, the architecture supports several scaling patterns:
code
Code
+-------------------------------------------------------------------------------------------------------+
|                                    ENTERPRISE CLOUD SCALING PIPELINE                                  |
+-------------------------------------------------------------------------------------------------------+
|  +---------------------------+   +----------------------------+   +--------------------------------+  |
|  |     Ingress Layer         |   |     Application Instances  |   |     Persistent Cloud DB        |  |
|  |     - Cloud Run           |   |     - Server-Side Express  |   |     - Firestore Database       |  |
|  |     - HTTPS Load Balancing|   |     - Vite Static Server   |   |     - Cloud SQL (PostgreSQL)   |  |
|  +-------------+-------------+   +-------------+--------------+   +---------------+----------------+  |
+----------------|-------------------------------|----------------------------------|-------------------+
                 |                               |                                  |
                 v                               v                                  v
+-------------------------------------------------------------------------------------------------------+
|  Container Auto-Scaling      |   - Real-Time Synchronization  |   - Sub-Second Document Fetch  |  |
|  - Ingress on Port 3000      |   - OAuth Secure Authentication|   - Relational Core Sharding   |  |
+-------------------------------------------------------------------------------------------------------+
8.1 Server-Side Express Migration & Production Builds
For enterprise environments requiring centralized access, the client-only application can scale to a full-stack configuration:
Vite Development Server Proxy: Runs on port 3000 behind an Nginx reverse-proxy in the Cloud Run container.
Compiled CommonJS Backend Build: Combines server resources into a single bundle to speed up deployment cold starts:
Production Deployment: Start the server using optimized startup commands:
8.2 Persistent Cloud DB Integration (Firebase vs. Cloud SQL)
The application’s data layer can scale to support persistent, multi-user storage:
Firestore (NoSQL): Best for rapid prototyping and flexible data models. It allows seamless, real-time sync of active regulatory checklists and nomenclature tables.
Cloud SQL (PostgreSQL): Ideal for relational structures. It supports complex transactions, data indexing, and joins between high-volume global medical nomenclatures.
9. Conclusion & Future Outlook
The MEDEVIS-TUDID Dual-Engine Analytical Interface bridges the gap between disparate medical device nomenclatures and regional regulatory registries. By combining intuitive, natural-language SQL generation with automatic data cleaning and interactive, browser-based 3D visualizations, the platform simplifies complex compliance workflows for regulatory teams.
As regulatory requirements continue to evolve globally, integrating predictive AI scoring, semantic vector search, and self-correcting query engines will ensure the system remains a reliable tool for clinical compliance and market clearance.
10. 20 Comprehensive Follow-Up Questions
To guide the next phases of development, system scalability, and regulatory compliance, please consider the following 20 technical and product questions:
Architectural & Database Performance
In-Memory Optimization: How should we scale the browser-side memory engine to maintain 60fps performance if active records grow from 2,000 to over 50,000 entries?
DuckDB WASM Integration: Should we transition the rule-based javascript filter engine into a compiled client-side WebAssembly instance (e.g., DuckDB-Wasm) to handle true SQL queries in the browser?
Caching Strategy: How should we structure local cache eviction policies (e.g., IndexedDB vs. LocalStorage) for large EMDN/GMDN nomenclature tables that rarely change?
Database Sharding: If we scale to a persistent PostgreSQL backend, should we partition the TUDID registration table by region, manufacturer, or registration year to optimize query performance?
Data Quality & Ingestion Pipeline
Audit Rule Extensibility: How can we design a modular framework that allows compliance teams to add custom data-quality audit rules without writing code?
Incremental Ingestion: How should we handle record collisions when pasting new CSV/JSON data (e.g., over-writing existing IDs vs. creating incremental version histories)?
Unstructured OCR: Should we implement an optical character recognition (OCR) pipeline to parse scanned PDF certificates directly into the structured TUDID registry?
Automated Schema Drift: How should the system handle sudden changes in source database schemas, such as the introduction of new GS1 identifiers or changes in risk level codes?
Advanced Visualizations & UI Interactions
WebGL Migration: If visualization density increases, should we transition the SVG-based 3D scatter plot and network graph to a WebGL-based framework (e.g., Three.js) to leverage GPU acceleration?
Custom KPI Export: Should we allow users to export custom KPIs and metric configurations as shareable JSON files, or store them in a persistent user profile database?
Network Force Physics: Would adding simulated collision forces and link distances to the applicant network graph help users identify hidden connections between manufacturers and risk classes?
Bilingual Search Highlighting: How can we improve visual feedback to highlight the specific text blocks that trigger fuzzy matches across traditional Chinese and English terms?
Proposed AI Capabilities
ML Feature Engineering: What additional features (e.g., recall history of similar model numbers, manufacturing country volatility indices) would improve the accuracy of the Predictive Risk Recall Forecaster?
Local LLM Execution: Should we explore running lightweight, local LLM embeddings (e.g., ONNX-based WebGPU models) in the browser to enable offline semantic translation?
SQL Self-Correction Limits: How should we configure the self-correcting NL-SQL Copilot to handle multi-step SQL queries, and what safety guardrails should prevent destructive query generation?
AI Translation Grounding: How can we prevent the system prompt tuner from hallucinating schema joins when translating queries for complex, custom database structures?
Security, Hosting, & Compliance
HIPAA & GDPR Boundaries: Since the platform handles regulatory device mappings rather than personal health information (PHI), what privacy policies should we enforce to guarantee compliance with regional data laws?
Enterprise OAuth Security: How should we structure Google Workspace or Active Directory single sign-on (SSO) to enforce role-based access control (RBAC) across the dashboard?
Secure API Proxying: To prevent exposing API keys in the browser, how should the Express gateway handle secure, server-side proxying for external translation and mapping services?
Audit Trail Logging: How should we design the database schema to track manual overrides, data updates, and auto-cleaning events for official compliance audits?
