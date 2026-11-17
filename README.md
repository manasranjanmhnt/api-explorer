<img src="website/reqzen-mark.svg" alt="Reqzen logo" width="56">

# Reqzen — API Explorer and Desktop API Client

Turn unfamiliar API source code into something you can explore and use. Reqzen scans supported Java, JavaScript/TypeScript, and Python API projects into a searchable catalog, then gives you a focused desktop workspace to inspect endpoints, prepare requests, and send them only after review.

Built for developers onboarding to an existing service, investigating API contracts, or keeping repeatable requests close to their project. Reqzen runs as a local-first desktop app: no Reqzen account or hosted catalog is required, and core scanning, browsing, and request workflows work without AI.

## Install Reqzen

You need only the installer for your operating system. The app and its runtime are included; **Node.js, npm, Git, Python, Java, and a separate frontend are not required to install or run Reqzen.**

Use the [Reqzen Download page](https://manasranjanmhnt.github.io/reqzen/) to choose Windows or macOS and get the matching latest installer. Mac users can select Apple silicon (ARM64) or Intel (x64). The page labels each download and links directly to the official GitHub release asset.

You can also use the [GitHub Releases](https://github.com/manasranjanmhnt/reqzen/releases) page. New releases label the operating system and processor in each filename. Older releases use these suffixes: **Windows x64** ends in `-x64.exe`, **macOS Apple silicon (ARM64)** ends in `-arm64.dmg`, and **macOS Intel (x64)** ends in `-x64.dmg`. Install and launch the app using the instructions for your operating system below.

Download installers only from the official Releases page. If it does not list an installer for your operating system, wait for an official package rather than using an unofficial mirror.

### Windows

1. Run the downloaded `Reqzen-<version>-x64.exe` file.
2. Follow the installer prompts.
3. Start **Reqzen** from the Start menu.

The Windows installer is unsigned, so SmartScreen may show a warning. Proceed only if you downloaded the installer from the official Releases page and trust it.

### macOS

1. Open the `.dmg` file for your Mac’s processor: `arm64` for Apple silicon or `x64` for Intel.
2. Drag **Reqzen** into **Applications**.
3. Open Reqzen from Applications.

The macOS packages are unsigned and not notarized, so macOS may block the first launch. Only proceed if you downloaded Reqzen from the official Releases page and trust the download. In Finder, Control-click Reqzen, choose **Open**, and confirm. If macOS still blocks it, go to **System Settings → Privacy & Security**, scroll to the Security section, and choose **Open Anyway** for Reqzen.

## What Reqzen helps you do

- **Find APIs in source code.** Scan a local project or a GitHub repository without building or running that project.
- **Explore a searchable API catalog.** Review services, operations, methods, paths, parameters, descriptions, and available contract details.
- **Prepare requests with context.** Set up environments, tokens, variables, headers, query and path parameters, and request bodies.
- **Review before sending.** Use HTTPS environments and inspect requests before they go out; the app does not send requests automatically.
- **Reuse and share your work.** Save custom requests and collections, import or export workspaces, and export collections in Postman v2.1 format.
- **Use the AI provider that fits your workflow.** Choose Ollama, Claude, or any OpenAI-compatible local or hosted service, including Groq, for AI-assisted search, request planning, and documentation.

### Supported source patterns

Reqzen includes scanning support for Spring Boot (Java), NestJS and Express-style routes (JavaScript/TypeScript), and FastAPI and Flask route decorators (Python). Custom annotation and decorator rules can adapt scanning to other source patterns. Scanning is static: dynamically assembled routes, framework-specific router mounting, and unsupported conventions may not be detected. Review the scan report and catalog before relying on the results.

## Your first session

1. **Choose a starting point.** Scan a local project, open a compatible catalog snapshot, scan a GitHub repository, or create a custom request. You do not need a catalog to create a request.
2. **Explore the API.** Search the catalog and open an operation to inspect its method, path, parameters, and contract details.
3. **Add an environment before sending.** Go to **Settings → Environments** and add a clear name and HTTP or HTTPS base address, or use an environment from your snapshot. HTTPS API requests are restricted to hosts in enabled environments; HTTP API and token requests can use any host.
4. **Set up authentication if needed.** Enter a session access token, configure a token type, or use the supported authorization options for a custom request. A token type can use a catalog API or a manually configured HTTP or HTTPS token request.
5. **Review, then send.** Choose the environment, check the complete request, and send it when you are ready. Write operations, production environments, or incomplete API contracts may require extra confirmation.
6. **Keep what you’ll reuse.** Favourite APIs, create collections, save custom requests, or export a collection or workspace.

### Request safety and local data

HTTPS API requests must use a host allowed by an enabled environment or service override. Token requests can use any host over HTTP or HTTPS, and HTTP API requests can use any host. HTTP traffic—including authorization credentials—is unencrypted and may be visible to others on the network. Use HTTP only on trusted development networks. The app checks requests before sending them and may require confirmation for write operations, production use, or incomplete API contracts. It does not send requests automatically.

Environments, variables, collections, preferences, and other workspace settings are stored on this computer. Access tokens entered for API requests stay in memory while the app is open. Token-type configuration and other locally saved settings may contain sensitive values and are stored in local files; avoid configuring secrets on shared computers and protect your operating-system account. Exported workspaces and collections may contain project information—review files before sharing them.

See the [Privacy Policy](docs/PRIVACY.md) for details about local storage, API requests, GitHub scans, and optional model providers.

### AI credential privacy

**Reqzen keeps known API access tokens and `Authorization` credentials out of AI prompts.** Before sending prompts to Ollama, Claude, Groq, or another configured OpenAI-compatible provider, it redacts known request credentials and common token or secret patterns. This applies to AI-assisted search, request planning, and documentation agents, whether the model is local or hosted.

AI provider keys are separate: they are sent to the configured provider only for endpoint authentication, not included in the prompt, and are held in memory for the current session. AI prompts can still contain relevant API contract details, search questions, request descriptions, and your AI instructions. Redaction is a safeguard, not a way to make arbitrary text safe; do not paste secrets into descriptions or custom AI instructions. For hosted models, review what prompt information the selected provider receives and its policies.

## Optional integrations

- **Git:** install Git if you use repository-cloning workflows. Local-folder scanning does not need Git. GitHub API scanning needs an internet connection; private repositories require appropriate access.
- **AI models:** AI is optional. Basic scanning, catalog browsing, and request building work without a model. In **Settings → AI model and provider**, choose:
  - **Ollama** for local inference. Install Ollama and download a model such as `qwen2.5:3b`; the app uses that model by default. You can set `OLLAMA_CHAT_MODEL` to use another installed model.
  - **OpenAI-compatible** for local model servers such as LM Studio, Ollama's OpenAI-compatible endpoint, llama.cpp, vLLM, or LocalAI, or for hosted services such as Groq. Enter the server's base URL and model ID, or use **Use Groq** to prefill Groq's endpoint. Use **Load available models** to discover model IDs, then select and save one. The server must support OpenAI-compatible `/models` and `/chat/completions` endpoints with JSON response mode. Remote servers require HTTPS.
  - **Claude API** for Anthropic models. Enter an API key in settings.

  Keys are kept in memory for the current app session and are not saved to disk; enter them again after restarting Reqzen. Reqzen redacts known API access tokens and authorization credentials from prompts before sending them to any model. When you select a hosted provider such as Groq or Claude, relevant API metadata, search questions, request descriptions, or writing instructions are sent to that provider. Review the [Privacy Policy](docs/PRIVACY.md) and your organization's AI-use rules before enabling a hosted model.

## For developers: run from source

### Requirements

- Node.js 22.12 or newer and npm.
- Windows 10/11 64-bit to build the Windows installer.
- macOS to build a macOS disk image. Build x64 on an Intel Mac or arm64 on an Apple-silicon Mac; the release workflow builds both.
- Git only for workflows that clone GitHub repositories. Local-folder scanning does not require Git.

The compiled app UI is included; no separate frontend build is required. You do not need Python, Java, or any of the scanned languages installed to run the app. A scanned project's dependencies do not need to be installed because scanning reads source files statically.

### Clone, install dependencies, test, and run

Open PowerShell on Windows or Terminal on macOS:

```sh
git clone https://github.com/manasranjanmhnt/reqzen.git
cd reqzen
npm ci
npm test
npm start
```

Run npm commands from the repository root (the directory containing `package.json`). `npm ci` installs the locked development dependencies; `npm test` runs the automated test suite; `npm start` launches the app from source.

### Automated security checks

GitHub Actions runs CodeQL analysis for JavaScript/TypeScript and workflow code, audits the npm lockfile for high- and critical-severity advisories, and scans repository history for exposed credentials with Gitleaks. The PR checks also run the test suite with a minimum line-coverage threshold of 90%. Set the `TEST_COVERAGE_THRESHOLD` Actions repository variable to change that percentage. These checks run on pull requests to `main` and on a weekly schedule; CodeQL, dependency audits, and test coverage also run on pushes to `main`.

### Build a Windows installer

Build on Windows, from PowerShell in the repository root:

```powershell
npm ci
npm test
npm run dist:win
```

The installer is written to `release\` as `Reqzen-<version>-x64.exe`. The installer is unsigned, and executable signing/resource editing is disabled during packaging. Build Windows packages on Windows rather than relying on cross-platform packaging.

### Build macOS disk images

Build on a Mac, from Terminal in the repository root:

```sh
npm ci
npm test
npm run dist:mac
```

The `.dmg` is written to `release/` and targets the Mac's architecture. To build the other architecture too, run `npm run dist:mac -- --x64` or `npm run dist:mac -- --arm64`. Both architectures are built in the release workflow. The packages are unsigned and not notarized.

For signed and notarized distribution, an Apple Developer ID Application certificate and app-specific password are required. See the [macOS build and signing guide](docs/MACOS.md); never commit signing credentials or store them in project files.

## Why developers use Reqzen

When an API is unfamiliar, the work is scattered: find its routes in source, understand its contract, configure a client, and keep useful requests for later. Reqzen brings those steps into one desktop API explorer and API client.

- **Go from source to endpoints faster.** Build a browsable catalog from supported source patterns without first deploying the service.
- **Keep discovery and testing connected.** Inspect an operation, configure an environment, and prepare a request in the same app.
- **Stay in control of requests.** HTTPS and enabled-environment host checks help constrain destinations, while review and confirmation steps keep sending intentional.
- **Adopt it without a hosted setup.** Install the desktop app and start with a local project or catalog; core features do not depend on AI or a Reqzen account.
- **Take your work with you.** Export Postman v2.1 collections or Reqzen workspaces to fit your existing workflow.

Reqzen is an API source code scanner, searchable API catalog, and desktop API client for developers working with Spring Boot, NestJS, Express-style routes, FastAPI, and Flask. Scan results and generated documentation are starting points for developer review, not a substitute for it.

## Platform guides

- [Windows setup and build](docs/WINDOWS.md)
- [macOS setup, build, and signing](docs/MACOS.md)
- [Privacy Policy](docs/PRIVACY.md)

## License

The code in this repository is licensed under the [MIT License](LICENSE). Third-party dependencies and bundled components remain subject to their own licenses.

## Public repository hygiene

Do not commit API snapshots, exported workspaces, environment addresses, credentials, signing secrets, or local test output. The `.gitignore` excludes common generated and sensitive files; review every file before publishing.
