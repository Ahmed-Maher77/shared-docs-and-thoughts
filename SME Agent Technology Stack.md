# SME Agent: Technology Stack

The SME Agent is our content creation agent. It interviews subject-matter experts (SMEs), turns what they say into briefs and articles, and saves the approved content in a **Content Hub** so the team can find and reuse it later.

This page lists the tools we use and what each one does for us.

---

## How It Works

1. **Request:** a **Content Creator** (or an **Admin**) creates a content request and assigns an SME to it.
2. **Brief:** the AI writes a brief, and the Content Creator reviews and approves it.
3. **Interview:** the SME is interviewed in a Teams meeting or by voice inside the app, or an existing transcript is uploaded.
4. **Facts:** the AI pulls the key facts out of the interview, and the **SME** checks and approves them.
5. **Article:** the AI drafts the article from the approved facts, and the Content Creator refines it with the AI editing assistant.
6. **Content Hub:** the Content Creator publishes the approved article to the Content Hub, where the team can find and reuse it (for example, the **Design Team** builds visuals from it).

### Roles

| Role | What they do |
| --- | --- |
| **Admin** | Can do everything, and also manages users, roles and settings. |
| **Content Creator** | Creates requests, assigns SMEs, approves their own briefs, edits their own articles, and publishes and reuses content. |
| **SME** | Checks and approves the facts and accuracy of the work assigned to them. |
| **Design Team** | Views the content in the Content Hub (read only). |

---

## 1. The Web App

| Tool | What it does for us |
| --- | --- |
| **Next.js 16** | The main framework. It serves both the web pages and the backend API from one project. |
| **React 19** | Builds the user interface. |
| **TypeScript** | JavaScript with types, which catches many mistakes before the code runs. |
| **Tailwind CSS + shadcn/ui** | Styling and ready-made UI components (buttons, dialogs, forms). |
| **Zod** | Checks that incoming data, and every AI response, has the expected shape before we use it. |

---

## 2. AI (Writing and Editing)

| Tool | What it does for us |
| --- | --- |
| **OpenAI (GPT-4o)** | The language model that writes briefs and articles and answers editing requests. We can switch models in config. |
| **Vercel AI SDK** | The library our code uses to talk to OpenAI. It also runs the editing agent, which can use tools to update an article. |

We log the token usage, response time and prompt version of every AI call so we can track quality and cost.

**Privacy:** during the in-app interview, names and other sensitive details are masked before the text goes to OpenAI and restored when the answer comes back. Extending this masking to every AI call is planned.

---

## 3. Voice Interview

SMEs can be interviewed by voice inside the app.

| Tool | What it does for us |
| --- | --- |
| **Whisper (runs in the browser)** | Turns the SME's speech into text on their own device, so their raw audio never leaves it. |
| **Silero VAD** | Detects when the SME starts and stops talking. |
| **OpenAI Text-to-Speech** | Reads the agent's questions out loud. The audio starts playing while the rest is still being generated. |

---

## 4. Data and Files

| Tool | What it does for us |
| --- | --- |
| **PostgreSQL** | The main database: requests, interviews, facts, articles and users. |
| **Prisma** | Lets our code read and write the database safely and manages changes to the database structure. |
| **File storage (S3-compatible)** | Stores uploaded attachments and generated PDF briefs. |

---

## 5. Sign-in and Microsoft Integration

| Tool | What it does for us |
| --- | --- |
| **Microsoft Entra ID (company login)** | Users sign in with their work Microsoft account. |
| **Role-based access** | Each role (Admin, Content Creator, SME, Design Team) sees and does only what it is allowed to. Permissions are checked again on every request. |
| **Microsoft Graph** | Schedules interviews in Outlook and finds SMEs in the company directory. |
| **Recall.ai** | Sends a bot to live Teams meetings to record the interview transcript. |

---

## 6. Testing and Quality

| Tool | What it does for us |
| --- | --- |
| **Vitest** | Unit tests for individual pieces of logic and UI. |
| **Playwright** | End-to-end tests that click through the app like a real user. Results link to Azure DevOps test cases. |
| **DeepEval** | Scores AI output (briefs, articles, interview questions) so we notice when a prompt or model change makes quality worse. |
| **ESLint + Prettier** | Keep the code style consistent. They run automatically before each commit. |

---

## 7. Hosting

| Tool | What it does for us |
| --- | --- |
| **Vercel** | Hosts the app. Every deploy updates the database structure automatically. |
| **Railway** | Another hosting setup. If a database update fails, the previous version stays live. |
| **Docker** | Runs the app and database on a developer's machine. |

### Hosting Notes
- **Vercel:** the app is sometimes slow and not always stable on Vercel.
- **Railway:** more stable in our experience. However, Railway had a security incident in which AI API keys stored on the platform could be stolen. Railway is working on a fix. Until it is confirmed fixed, keep the API keys rotated and set spending limits on them.

---

## 8. Coming Next

- **Smarter fact grounding:** search over past content (pgvector) so the AI relies on verified sources.
- **Background jobs:** long tasks keep running reliably and resume if something fails.
- **AI gateway:** one central place for every AI call, handling model choice, fallbacks, spending limits and monitoring.
- **Cost and performance monitoring:** dashboards for AI cost and app health.
- **Email notifications** through Microsoft Graph.
- **Privacy masking on every AI call:** hide names and sensitive details before any text goes to OpenAI.
