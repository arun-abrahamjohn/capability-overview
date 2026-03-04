# Capability Overview

**Live demo:** https://arun-abrahamjohn.github.io/capability-overview

A single-page interactive tool for presenting your professional skills and exploring project fit — in real time, with whoever you're talking to.

---

## What it's for

Static CVs and capability decks are one-way. This is designed for the moment when someone needs to quickly understand what you bring — and whether you're right for a specific piece of work.

The idea: you set up your skills beforehand. Then, in a conversation with a potential client, staffing lead, or collaborator, they describe a project type and the tool immediately generates a contextual read of how your skills apply to it. Which capabilities are relevant, how they map to the work, and what contribution you'd make.

It's built for consultants, designers, researchers, and other specialists who are regularly being considered for project work and want something more dynamic than a PDF to facilitate that conversation.

---

## How it works

**Before the conversation**

1. Add your skills — name, proficiency level, and a short description of what you can actually do with each one
2. Add any additional context (working style, constraints, how the AI should represent you)
3. Optionally add a few project types yourself to seed the view

**During the conversation**

The other person describes a project scenario in plain language. The tool:

- Validates it as a legitimate project type
- Generates a project label and a contextual description
- Automatically identifies which of your skills are relevant
- Writes a short paragraph on how you'd contribute to that specific engagement

Selecting a project shows a response panel with the title, description, and the relevant skill cards expanded. Previously generated responses are cached — no repeat API calls for the same project.

**After**

Skills and projects persist in the browser. You can return to the same view, add more, or clear everything and start fresh.

---

## Getting started

No installation. No build step. No backend.

1. Download or clone this repository
2. Open `index.html` in any modern browser
3. Enter your Anthropic API key when prompted (see below)
4. Add your skills and context
5. Start adding project types

That's it.

---

## API key

This tool calls the [Anthropic API](https://docs.anthropic.com) directly from the browser using the `claude-sonnet-4-20250514` model.

You'll need an API key from [console.anthropic.com](https://console.anthropic.com). When you open the tool, you'll be prompted to enter it. The key is stored in your browser's `localStorage` only — it is never written to any file, never sent anywhere except Anthropic's API, and will not appear in any Git commit.

**Your API key is safe to share this repo publicly.** There is no `.env` file, no config file, no place in the code where a key could accidentally be committed.

To remove your key from the browser, click **Remove API key** in the footer.

### API usage and cost

Each call uses `claude-sonnet-4-20250514`. Token caps per call:

| Action | Max output tokens |
|---|---|
| Intro generation | 120 |
| Skill / project validation | 150 |
| Project generation | 1000 |
| Project response (first view) | 1000 |
| Skill-to-project assignment | 300 |

Responses are cached after first generation. Switching between previously viewed projects makes no additional API calls.

---

## Sharing and hosting

### Share as a GitHub Pages link

The simplest way to share this in a portfolio or send to someone:

1. Push `index.html` and `README.md` to a public GitHub repository
2. Go to **Settings → Pages** in the repo
3. Set source to **Deploy from a branch**, select `main`, root `/`
4. GitHub will give you a public URL like `https://yourusername.github.io/capability-overview`

Anyone who opens that link gets a fresh, blank instance in their own browser. They'll need their own Anthropic API key to use it.

### Share a pre-filled version

If you want to share your skills already loaded — for example, to let someone explore your profile before a meeting — open the tool, set up your skills and context, then share the link. Your data lives in your browser's localStorage and won't transfer, but the page will be empty for them. For a pre-filled shareable version, the simplest approach is to export your data as a JSON snapshot and document how to import it, or host a version with the data baked in.

---

## Usage guide

### Additional Context

Click **Context** in the footer. Write freely — working style, constraints, how you prefer to collaborate, anything the AI should factor into how it describes you. This is not shown anywhere in the UI; it shapes AI outputs silently.

### Adding skills

Click **+ Add skill** in the chips row. Each skill needs:

- A name (must be unique)
- A description of what you can actually do with it
- A proficiency level: Expert, Proficient, or Foundational

The AI validates new skills before they're added and will flag anything that doesn't read as a professional capability. It also checks whether the new skill is relevant to any existing projects and adds it to matching ones automatically.

### Adding project types

Click **+ Add project type** below the project list. Describe a scenario in plain language — for example: *"Discovery research for a complex B2B SaaS product with multiple stakeholder groups."*

The AI will:
1. Validate it as a real project scenario
2. Generate a project label and a contribution description
3. Match your relevant skills to it

### Selecting a project

Click any project button to see your response. The first time generates a fresh AI response; subsequent clicks use the cached version instantly.

Use the **Reset** button (appears below the project list when a project is selected) to deselect and return to the placeholder.

### Clearing data

Click **Clear data** in the footer to remove all skills, projects, and context from the browser. This cannot be undone.

---

## Tech

One file. No framework. No build tool. No dependencies.

| | |
|---|---|
| UI | Vanilla HTML, CSS, JS |
| AI | Anthropic Claude API (direct browser call) |
| Storage | Browser `localStorage` |
| Font | Plus Jakarta Sans (Google Fonts) |

Dark mode by default. Light mode toggle in the header.

---

## License

MIT
