# Generation Notes

Mode: ai

Model: groq / llama-3.1-8b-instant

Fallback reason: None

Architecture: Real Estate Policy Assistant

Template path: templates/simple-rag/real-estate-policy-assistant

Short description:

A beginner-friendly Simple RAG (Red, Amber, Green) project for Human Resources Escalation Triage

Architecture notes:

- Use a microservices architecture to improve scalability and maintainability
- Implement a caching layer to improve performance
- Use a message queue to handle asynchronous tasks

Project planner agent workflow:

- Architecture Agent: Define app boundaries, data flow, runtime stack, and integration points. Outputs: Use a microservices architecture to improve scalability and maintainability; Implement a caching layer to improve performance; Use a message queue to handle asynchronous tasks
- Backend Agent: Design FastAPI modules, service contracts, validation, and error handling. Outputs: NLP Module; Knowledge Graph Module; Database Module; API Gateway Module
- Frontend Agent: Design React screens, state flow, controls, and user feedback states. Outputs: User Interface; Input Form; Output Display
- Database Agent: Design persistence models, sample data, indexes, and audit records. Outputs: Run history; Source document metadata; Generated workflow audit records
- Testing Agent: Define contract tests, smoke tests, and generated project validation. Outputs: Unit testing, Integration testing, and End-to-end testing
- DevOps Agent: Define environment variables, Docker workflow, and repository packaging. Outputs: Docker-ready project; Environment sample file; GitHub repository upload
- Reviewer Agent: Review the generated plan for completeness, security, and portfolio quality. Outputs: Identify employee concerns; Analyze employee feedback; Escalate issues to higher management; Monitor and evaluate employee satisfaction
