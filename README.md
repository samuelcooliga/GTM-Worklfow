1. LLM Enum Constraints (Schema Enforcement)
To prevent the CRM from rejecting malformed data, the AI prompt is engineered with strict Enum constraints. Rather than allowing the LLM to generate unstructured text, it is forced to act as a deterministic classifier, outputting exact HubSpot picklist values (e.g., COMPUTER_SOFTWARE) to ensure 100% database schema compliance.

2. API Failsafe & Rate Limit Resilience
Engineered to handle volatile third-party services and free-tier API quotas. Implemented sequential node execution (throttling) and exponential auto-retry loops to gracefully handle 429 Resource Exhausted and 503 Service Unavailable errors without crashing the pipeline.

3. Dynamic Data Wrangling
Utilized native JavaScript inside n8n expressions to handle edge cases in the data payload. This includes dynamically parsing stringified LLM outputs back into functional JSON objects and filtering out invalid characters/protocols from URLs before CRM injection.

4. Decoupled Development Architecture
Maintained forward momentum during upstream API outages (e.g., JSearch gateway failures) by building a decoupled architecture. Swapped failing HTTP requests with hardcoded Mock JSON payloads to continue engineering the AI and CRM layers, demonstrating pragmatic, unblocked problem-solving.

 How to Deploy
Import the workflow.json file into your n8n workspace.

Add your Google Gemini API key to the n8n credentials manager.

Generate a HubSpot Private App Token with crm.objects.companies.write permissions and link it to the HubSpot node.

Execute the pipeline.
