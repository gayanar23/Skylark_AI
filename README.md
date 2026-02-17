Skylark OPS – Drone Operations Coordinator AI



Skylark OPS is a single-page AI-powered drone fleet management system designed to simulate the role of a real-world Drone Operations Coordinator. It combines conversational AI, deterministic business logic, conflict detection, assignment tracking, and Google Sheets integration into a single production-style application.



The goal of this system is to manage pilots, drones, and missions while automatically detecting operational conflicts and assisting decision-making through AI-based reasoning.



System Overview



Skylark OPS is built as a single-page application (SPA) using HTML, CSS, and JavaScript. It integrates deterministic rule-based validation with AI-powered reasoning through the Claude model via OpenRouter.



The system performs the following core operations:



Pilot roster management



Drone inventory management



Mission tracking



Assignment coordination



Conflict detection



Budget and cost analysis



Weather-based operational validation



Optional Google Sheets synchronization



Architecture Overview



The system follows a layered architecture even though it is implemented inside a single HTML file.



High-Level Architecture:



Frontend UI (Chat, Dashboard, Data Tables)

↓

In-Browser Business Logic Engine (JavaScript)

↓

Deterministic Conflict Detection Layer

↓

System Prompt Context Injection

↓

Claude API (LLM via OpenRouter)

↓

State Update and Optional Google Sheets Write-Back



Architectural Layers Explained

1\. Presentation Layer (Frontend UI)



Built with HTML5, CSS3, and Vanilla JavaScript.



This layer provides:



Conversational AI chat interface



Data tables for missions, pilots, and drones



Conflict board



Analytics dashboard



Modal forms for adding data



Live alert feed



Decision log documentation



It is responsible for user interaction, state rendering, and visual indicators.



2\. Business Logic Layer (Deterministic Engine)



All mission-critical logic runs inside JavaScript. The AI model does not perform calculations or enforce rules.



This layer handles:



Assignment validation



Cost calculation



Date overlap detection



Location matching



DGCA certification validation



Weather compatibility checks



Budget validation



Status transitions (Available → Deployed)



This ensures predictable and reliable operations without AI hallucination.



3\. Conflict Detection Engine



Every assignment is validated against six predefined rules:



Pilot double booking (date overlap logic)



Missing DGCA certification



Drone under maintenance



Budget overrun



Location mismatch



Non-rain-rated drone assigned to rainy mission



Date overlap formula used:



NOT (end1 < start2 OR start1 > end2)



Conflicts are surfaced in:



Conflict board



Data table badges



Live alert feed



4\. AI Reasoning Layer



Claude (via OpenRouter) is used for:



Natural language understanding



Assignment recommendations



Operational summaries



Fleet status explanations



Cost breakdown explanations



Urgent reassignment reasoning



Important design decision:



All numeric validation and rule enforcement are deterministic.

AI is used only for reasoning, explanation, and recommendation.



5\. Google Sheets Integration



The system can read data from Google Sheets using Sheets API v4.



Expected sheet tabs:



Pilot\_Roster



Drone\_Fleet



Missions



If API keys are not configured, the system uses seeded fallback data.



Write-back requires OAuth configuration. If OAuth is not set, updates remain in in-memory state only.



Functional Modules

Pilot Roster Management



Filter by skills and location



DGCA certification validation



Availability tracking



Assignment history



Cost calculation (days × daily rate)



Drone Inventory Management



Capability filtering



Maintenance tracking



Weather rating validation



Location-based matching



Deployment status control



Mission Management



Mission creation



Priority levels (Normal, High, Urgent)



Required skill enforcement



Budget tracking



Weather forecast handling



Conflict Management



Automatic conflict detection



Manual conflict logging



Severity levels (Warning, Critical)



Global conflict re-scan



Cost Calculation Logic



Mission duration is calculated using start and end dates.



cost = number\_of\_days × pilot\_daily\_rate



Budget rules:



Above 80% of budget → Warning



Above 100% of budget → Critical



Design Philosophy



The architecture intentionally separates deterministic validation from AI reasoning.



This ensures:



Reliability in operations



Prevention of AI-based calculation errors



Clear rule enforcement



Explainable decisions



Expandability to production systems



The system demonstrates strong coordination logic suitable for real-world drone fleet operations.



Tech Stack



Frontend: HTML, CSS, Vanilla JavaScript

AI Model: Claude (claude-sonnet-4)

AI Gateway: OpenRouter

Data Source: Google Sheets API v4

State Management: In-memory JavaScript objects

Deployment: Static hosting



Project Structure



This is implemented as a single-file prototype:



skylark\_ops\_connected.html



Internally structured into:



UI components



Business logic



Conflict engine



AI integration



Sheets API integration



Dashboard renderer



Decision documentation



Assumptions



One pilot and one drone per mission



Google Sheets is the system of record



Capabilities must match both pilot and drone



Rain missions require IP-rated drones



Deterministic logic overrides AI suggestions



Future Improvements



If extended to production, the architecture would evolve into:



React frontend

FastAPI backend

PostgreSQL database

Redis cache

WebSocket-based real-time updates

Authentication and role-based access control

Audit logs and assignment history

Geospatial map visualization

