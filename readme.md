# Agentic Postman Template

I spend a lot of time writing APIs, but almost as much time manually documenting and testing them in Postman. A typical workflow involves painstaking manual setup (configuring verbs, environment variables, test scripts, and mock response examples) which becomes a massive time sink when code is frequently refactored.

To solve this, I automated the process of building Postman collections. By providing AI agents with strictly defined rules and workflows, they can now read the backend routes and generate complete, fully-documented Postman endpoints in minutes. 

Using this template repository, you can instruct an AI agent (like Antigravity, Cursor, or Claude) to "observe these new routes and generate the Postman endpoints." The agent will follow strict instructions embedded within the codebase to automatically generate the Collection 3.0 YAML files, place them in a dedicated `AI Generated` collection, and inject the necessary scripts and context. It is  standardized to ensure documentation portals and developer experiences remain top-tier.

## Getting Started

Postman v12 is Git-native from the ground up. Follow these steps to get started:

1. **Fork the Repository** to your own GitHub account.
2. **Clone the Repository** to your local machine:
   ```bash
   git clone git@github.com:your-username/your-forked-repo.git
   ```
3. **Open in Postman**: Open the Postman App (v12+).
4. **Connect Local Repo**: Use the "Open Local Git Repository" option in Postman and navigate to the folder you just cloned.
5. Postman will automatically read the `.postman` folder, the `postman/collections/` YAML files, and the `postman/environments/` files.
6. Create a new branch directly in Postman or your IDE when working on new endpoints, and commit changes straight to GitHub.

## AI-Assisted Endpoint Generation

The `.agent/` directory contains embedded rules and workflows to automatically guide your AI assistants. With Collection 3.0, the AI agents will generate modular `.yaml` files instead of manipulating massive JSON blobs.

### How to Generate Endpoints
When working within an AI-enabled IDE or pairing with an AI agent:
1. Instruct the AI to **"Generate a Postman endpoint for [Module/Route]"**.
2. The AI will parse your backend routes and automatically scaffold a new directory containing `.yaml` endpoint files inside the **"AI Generated"** collection (`postman/collections/AI Generated/`).
3. **Review and Move**: Once the AI finishes generating the `.yaml` endpoints, review them within Postman or your Git diff. If the configuration is accurate, move the new folder into the appropriate finalized collection directory.

**Automated AI Actions Include:**
- Mapping the endpoint URLs correctly utilizing the standardized environment variables within `postman/environments/`.
- Writing standard Postman scripts on `POST` requests to capture the newly created ID and store it in the `{{resourceId}}` environment variable.
- Stripping redundant `Authorization` headers to ensure endpoints cleanly inherit the collection-level bearer token.
- Populating available Query Parameters automatically with `disabled: true` to self-document APIs without cluttering the URL.

> **Note on Response Examples**: Example Generation is currently disabled across the `.agent` instructions. Attempting to embed mock response examples inside Collection 3.0 YAML structures previously crashed the importer due to internal formatting issues with the mock schemas. This functionality will be reintroduced in a future patch once the internal structure is resolved.

## Manual Authoring Conventions

If manual adjustments or the creation of endpoints are necessary, you **MUST** adhere to the standardized guidelines established in the repository rulebook.

**[Read the Postman Conventions Rulebook](.agent/rules/postman-conventions.md)**

### Quick Reference:
- **Utilize `{{resourceId}}`**: This temporary environment variable stores the ID of the most recently created item. Ensures subsequent GET, PATCH, and DELETE endpoints target `{{resourceId}}` rather than hardcoding static IDs.
