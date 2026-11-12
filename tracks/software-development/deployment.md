---
title: PrimeCloud Deployment Guide
parent: Software Development
grand_parent: Hackathon Tracks
nav_order: 5
---

# Software Development: PrimeCloud Deployment Guide

**PrimeCloud deployment is mandatory for Challenges A, B and C**, alongside
the original functionality and integrated DSA task. Deploy a small working
solution, not a static placeholder. A production architecture or custom
domain is not required.

A local-only application, a GitHub repository alone, or a static landing page
without the selected challenge's actual functionality is **insufficient**.
Submit the assigned PrimeCloud URL and demonstrate the main workflow there.

Use the
[official PrimeCloud documentation](https://primecloud.cloud/docs) and
[quickstart](https://primecloud.cloud/docs/quickstart) as the platform source
of truth. Follow their current console instructions if labels or procedures
change. The CLI examples below were checked against the official quickstart
on **12 November 2026**; they are illustrative, not a new CLI specification.

## 1. Prerequisites and access

Before deploying, prepare:

- A PrimeCloud account/workspace and permission to deploy in the assigned
  project/environment, confirmed through the organizer's approved access route.
- Your team's GitHub repository, chosen branch and known working commit.
- The project's dependency manifest/lockfile, runtime requirements and actual
  build/start instructions.
- The required environment-variable names and approved configuration values,
  with secret values supplied privately rather than committed to Git.
- A locally working application with an HTTP interface and `GET /healthz`.
- Non-sensitive sample inputs and expected outputs for your selected challenge.
- For B, an organizer-approved persistent remote database/storage arrangement.
- For C, approved inference access reachable from the hosted application.

Confirm available resources, trial eligibility/expiry, service permissions,
storage and any costs with the Technical Lead before provisioning. Public
plan examples are not event entitlements. Do not assume unlimited credits,
always-on availability, a particular database allocation or shared API keys.
Do not incur unapproved charges.

Use the official quickstart for account creation and the
[application documentation](https://primecloud.cloud/docs/applications) for
supported deployment types. Install only your project's required runtime and
dependencies; there is no universal language or framework for this track.

Raise missing access or dependencies early. Record the issue, but do not
substitute a local-only run for successful mandatory deployment.

## 2. Prepare the application for hosting

Before connecting the repository:

1. Run the application locally and confirm the selected challenge's core
   workflow works with permitted sample data.
2. Declare every required dependency and retain the appropriate lockfile.
   Do not rely on undeclared packages installed on one teammate's laptop.
3. Run the project's actual dependency/build process and resolve failures.
   Record the commands and required runtime version.
4. List the required environment variables and distinguish non-secret
   settings from credentials.
5. Remove hardcoded credentials. If real credentials were committed, revoke
   or rotate them through the authorized route; removing the latest copy
   does not invalidate an exposed secret.
6. Configure the HTTP server to use `0.0.0.0` and the runtime port described
   in section 5.
7. Implement and locally check `GET /healthz`, using the requirements in
   section 6.
8. Test normal inputs, relevant failure cases and the DSA integration before
   attempting the cloud build.

| Challenge | What must run through the hosted service |
|---|---|
| A | The actual reconciliation engine through a lightweight HTTP API or equivalent interface; accept supported inputs and expose reconciled, review and matching results. |
| B | The accessible application interface and synchronization backend, using approved persistent remote storage. Offline data remains durable on the device. |
| C | The RAG application/API, supplied-knowledge-base or ingestion workflow, implemented heap-based top-K retrieval, grounded generation and citations. |

Keep the scope small. A's CLI/library can remain the core engine, but must be
callable through the deployed interface. B's local development API is not the
final remote sync service. C's laptop-only Ollama instance is not a hosted
inference arrangement.

Do not require a large model inside the trial container. An approved external
inference endpoint is allowed; do not expose an unsecured laptop model server
to the internet or assume the container can reach your laptop's `localhost`.

## 3. Connect the GitHub repository

Choose the **Console or CLI** route. You do not need to use both. Both routes
still require the application, configuration and verification steps below.

### A. PrimeCloud Console

1. Follow the official quickstart to access the Customer Console and select
   or create the approved project/environment.
2. Use the documented Git/source deployment route to connect your GitHub
   repository. Grant only the repository access needed for the project.
   Never paste GitHub passwords or access tokens into source files.
3. Select the intended repository, branch and application directory when the
   deployment flow requests them. For a multi-directory repository, identify
   the directory containing the application manifest/build context.
4. Check the commit being deployed and record it for your submission.
5. Review the detected application configuration before building.

The official application guide describes **Auto-deploy on push**. Where it is
enabled, pushes to the connected branch can trigger builds and deployments.
Confirm the selected branch and setting, respect the submission freeze and
record the deployed commit; pushing to another branch is not proof that the
assessed application changed.

PrimeCloud documents detection of Dockerfiles, Procfiles and supported package
manifests. Use your actual project's supported format; you are not required
to add every format or install a CLI. If repository authorization is
unavailable, ask the Technical Lead to confirm a supported deployment route.

### B. PrimeCloud CLI

The [official quickstart](https://primecloud.cloud/docs/quickstart) currently
shows the installation, authentication and initialization commands below.
Run them from the intended project repository only after confirming the
approved account/workspace. Replace the illustrative application name
`my-app` with your own name.

**Installer safety:** the first command downloads and executes a remote
installer. Review the official installer and your machine's software policy
before running it. Do not run these commands automatically on a shared machine
or provide credentials to an unofficial installer.

```bash
curl -fsSL https://cli.primecloud.cloud/install.sh | bash
primecloud auth login
primecloud init --name my-app
```

Complete the build/start, port, health, environment and storage configuration
in sections 4-8 before deploying. Follow the current quickstart for any
project/environment prompts; initialization alone is not a successful build.

The same quickstart documents deploying a selected branch and watching status:

```bash
primecloud deploy --branch main
primecloud status --watch
```

Use your actual connected branch instead of `main` where different. Check the
resulting revision and logs, not just whether the command started. If the
installed CLI differs from these examples, consult the current official
documentation or the Technical Lead rather than guessing extra flags.

## 4. Configure build and start commands

The **build command** installs/prepares dependencies and compiles assets where
your project needs that step. The **start command** runs the long-lived HTTP
application. They must match your repository, not a copied command from an
unrelated framework.

- Follow your dependency manifest, lockfile, Dockerfile or Procfile and the
  current PrimeCloud application-configuration documentation.
- For an npm project, `npm ci` requires a matching lockfile;
  `npm run build` requires a defined build script; `npm start` requires a
  suitable start script. These are conditional application examples, not
  universal PrimeCloud commands or permission to create meaningless scripts.
- For other stacks, use their actual documented dependency/build/start
  commands. Record the working commands in the README.
- Ensure the start process remains running, serves the real application and
  reads runtime configuration. Do not substitute a build-only command,
  development-only placeholder or one-off CLI task for the HTTP service.
- Review logs for build/runtime errors and missing dependencies. Fix the
  cause rather than reporting a failed build as a successful deployment.

No universal runtime version or build command is imposed by this track.
Use a supported version compatible with your dependencies.

## 5. Bind the runtime port correctly

PrimeCloud's quickstart requires the HTTP server to bind to
**`0.0.0.0:$PORT`**, not `127.0.0.1`.

- `0.0.0.0` is the listen address inside the container.
- `$PORT` means the runtime port value; it is not a literal string to pass
  unchanged to your server.
- Read the port through your framework's environment/configuration mechanism
  and align it with the configured PrimeCloud **Target Port**.
- Do not assume a framework's default development port matches the platform
  configuration. Follow the current documented port/environment settings.

Binding only to loopback can make a running process unreachable by the proxy
and health probe. The public HTTPS URL is assigned by PrimeCloud; participants
do not need a custom domain or their own TLS setup.

### Graceful shutdown

Where applicable, handle **SIGTERM**: stop accepting new requests, allow
in-flight work to finish within the platform's shutdown window, and close
database pools and other connections cleanly. Do not acknowledge pending sync
work before it is durably applied.

The current quickstart documents a **10-second grace period** before forced
termination. Verify the current platform contract and do not assume unlimited
cleanup time. See the [quickstart](https://primecloud.cloud/docs/quickstart)
and [application runtime guide](https://primecloud.cloud/docs/applications).

## 6. Provide health checks

Implement **`GET /healthz`** and configure the deployment's health-check path
through the documented platform settings.

The endpoint should respond quickly, use appropriate status codes and expose
no secrets, credentials or sensitive diagnostic details. Explain what it
checks and distinguish process health from dependency readiness where
relevant. Avoid expensive model generation or a full dataset reconciliation
on every probe.

The current quickstart specifies an **HTTP 200-399 response within five
seconds**. Prefer a direct successful response such as HTTP 200; do not
redirect the health probe to an external login page or require interactive
authentication. Follow the current documented timeout and actual deployment
configuration if these change. Keep sensitive application operations
protected separately.

A successful health check proves neither the DSA implementation nor the core
workflow. Both require the separate functional verification below.

## 7. Environment variables and secrets

Environment variables are named settings supplied to the running application,
such as its port, database connection configuration or model endpoint. Your
application reads them instead of hardcoding deployment-specific values.
Some settings are public configuration; credentials and API keys are secrets.

Document required **variable names and purposes**, not real values. Configure
runtime settings using PrimeCloud's documented application/environment
controls. Its official documentation describes Vault-backed secret bindings;
use the supported secret-management/binding route for credentials.

Use the approved database's documented binding workflow where applicable,
rather than copying a plaintext connection string into the repository.
Consult [Security, Vault and access control](https://primecloud.cloud/docs/security)
and [application configuration](https://primecloud.cloud/docs/configuration)
for the supported controls.

- Keep database credentials, inference keys and other secrets server-side.
  Do not embed them in source, frontend bundles, sample data or build output.
- Ignore real local environment files in your project repository. Provide a
  non-secret example configuration and explain which values users supply.
- Use only approved credentials and services. Do not assume organizer keys
  or paid AI access are supplied.
- Do not expose secrets in health responses, logs, screenshots or demo videos.
  Redact deployment evidence before submission.
- If a secret is exposed, notify the organizer and revoke/rotate it through
  the authorized route; deleting a visible line is not sufficient.

Configure allowed origins and application access as needed for your actual
frontend/backend arrangement. Do not disable safeguards just to make a demo
request succeed.

## 8. Persistence and database considerations

Local device storage, container-local files and persistent remote storage are
different. Do not assume a file written inside a running container survives
replacement or redeployment.

PrimeCloud's application documentation describes containers as **stateless
and replaceable**. Choose storage according to the data, not merely where it
is easiest to write a file:

| Component | Purpose | Important distinction |
|---|---|---|
| Application container | Runs the HTTP application and its processing code. | An ordinary container-local path is not a durability guarantee. |
| Managed database | Stores structured records and supports the application's query/update model. | Requires an approved service, connection binding and schema/setup. |
| Persistent storage | Retains data through a documented, configured storage attachment. | Availability and attachment/mount configuration must be confirmed; not every directory is persistent. |
| Object storage | Stores file objects, such as permitted uploads or document sources. | It does not automatically implement a transactional record database or synchronization protocol. |

**Challenge B:** use an organizer-approved PrimeCloud persistent-storage or
managed-database arrangement for synchronized records and durable
processed-operation tracking. PrimeCloud documents managed databases and
persistent storage; confirm availability, binding and storage configuration
for the assigned environment rather than assuming a particular engine or
allocation.

Configure connections through the documented settings/secret bindings.
Initialize the required schema using the project's documented setup and safe
migration procedure. Preserve server-side idempotency across restarts as well
as the browser's pending queue and acknowledged-ID state.

**Challenge A:** a database is optional unless your design needs one. Explain
how results and review evidence are returned/exported or retained.

**Challenge C:** explain whether document sources, the retrieval index or
other state need persistence, are supplied with the deployment or are rebuilt.
Permitted static/supplied documents may be packaged with the application where
appropriate; additional paid infrastructure is not automatically necessary.

Reproducible stateless processing is acceptable where it meets the challenge;
do not claim durability for ephemeral files. Use only permitted, non-sensitive
documents and records.

Avoid destructive resets of shared services. Any restart/redeployment or
storage test must remain within your assigned resources and permissions.
**Do not purchase a managed database or storage add-on without organizer
approval.** The Organising Committee must confirm allocated services.

See the official [database guide](https://primecloud.cloud/docs/databases),
[storage guide](https://primecloud.cloud/docs/storage) and
[application configuration](https://primecloud.cloud/docs/configuration).

## 9. Challenge-specific deployment guidance

### A. Backend Data Reconciliation & Fuzzy Search

Keep the reconciliation engine as a backend workflow or CLI library if
preferred, but expose its **actual functionality through HTTP**. A minimal
API is sufficient:

- `GET /healthz` for the lightweight health check.
- `POST /api/reconcile`, or your documented equivalent, to accept supported
  sample input and return actual reconciliation results.

A polished frontend is optional. Document the request format, validation and
result structure so judges can use the hosted API.

**Hosted checks:** submit examples in at least two supported formats; inspect
reconciled records, matching scores/source references and ambiguous review
items/decisions. Verify invalid-input reporting, the integrated index and FIFO
review workflow rather than displaying canned output.

### B. Offline-First Resource Tracker

Deploy the application and its synchronization service. The frontend must
remain usable offline, and the sync endpoint must become reachable through
PrimeCloud when connectivity is restored.

| Part | Role |
|---|---|
| IndexedDB, PouchDB or equivalent device storage | Keeps records and pending work durable on the device; it is not the remote database. |
| Local operation queue | Retains ordered create/update/delete work, stable operation IDs and unacknowledged changes for retry. |
| Synchronization API | Validates and applies queued operations, handles acknowledgment/conflicts and prevents duplicate application. |
| Approved persistent remote store | Retains synchronized records and durable processed-operation tracking across backend replacement. |

**Hosted checks:** open the application and perform online operations; go
offline, create/edit/delete and reload; confirm local persistence; reconnect
and synchronize to the hosted backend. Use two independent sessions to show
conflict resolution, retry/lost-acknowledgment deduplication and deletion
handling. Check remote persistence across a permitted restart/redeployment.
Local persistence alone does not demonstrate remote synchronization.

### C. Purposeful Agentic AI / RAG Workflow

Deploy the actual RAG application or API: ingest permitted documents or use
the supplied knowledge base, perform the implemented heap-based top-K
retrieval, generate grounded responses and display supporting citations.
Keep retrieve -> synthesize -> cite -> done bounded.

An approved external inference endpoint is allowed. Ollama can support local
development, but a locally running model is not a deployed cloud inference
service. You are not required to host a full language model inside a limited
trial container. Store any model API credentials server-side through the
approved PrimeCloud configuration/Vault facilities.

**Hosted checks:** demonstrate a supported task with retrieved evidence and
citations, absent/insufficient evidence, and explicit model/retrieval-service
failure handling. Show that the live pipeline uses the heap-selected evidence;
a static chatbot screen or a prewritten answer is insufficient.

## 10. Deploy and verify

Use the Console or verified CLI route to deploy, then complete every check:

1. **Deployment succeeds:** the build and release finish successfully, not
   merely enter the queue.
2. **Workload is running:** confirm the platform reports a running/healthy
   application and that the intended revision is active.
3. **HTTPS URL works:** open the assigned URL from a browser/session
   independent of your local development server.
4. **Health check succeeds:** request `GET /healthz` and confirm the expected
   response within the documented timeout.
5. **Core functionality works:** run the challenge-specific checks above,
   comparing known sample inputs with expected and observed outputs.
6. **Dependencies connect:** verify required database/storage connections and,
   for C, approved inference access.
7. **Logs are clear of unresolved critical startup errors:** inspect both
   build and runtime logs and fix the underlying failures.
8. **Secrets remain protected:** confirm configuration works without exposing
   credentials in output, health responses, source or submission evidence.
9. **Deployment is reproducible:** record the GitHub revision and actual
   setup/configuration steps; confirm the same repository and documented
   settings can reproduce the application.

A previously healthy version may remain available after a failed rollout.
An accessible URL alone does not prove that the intended new revision
deployed successfully. Preserve sanitized status evidence, test time,
observed results and any limitations.

## 11. Troubleshooting

Use logs and the official
[troubleshooting runbooks and diagnostic guide](https://primecloud.cloud/docs/guides#troubleshooting-doctor)
before changing configuration blindly.

| Issue | What to check and do |
|---|---|
| Wrong application port | Compare the application's runtime port with PrimeCloud's Target Port and documented `$PORT` configuration. |
| Bound to localhost | Bind the HTTP server to `0.0.0.0`, not only `localhost` or `127.0.0.1`. |
| Missing dependencies | Declare the dependency in the manifest/lockfile and rebuild; a package installed only on a laptop is not available automatically. |
| Incorrect start command | Confirm the command exists, uses the right application directory and runs the HTTP process rather than only building assets or exiting. |
| Failed build | Read the first relevant build failure; fix dependency, runtime or build configuration before retrying. Do not report the old active version as the new build. |
| Missing environment variables | Compare required variable names with the approved runtime configuration; confirm secret bindings without printing secret values. |
| Database connection failure | Check the approved service, environment, binding, connection settings and schema/setup. Do not paste credentials into public logs or bypass access controls. |
| Health-check failure | Check the route, listen address, target port, response and timeout; avoid interactive login redirects and expensive model/data work in the probe. |
| Memory/resource errors | Inspect logs and metrics, reduce unnecessary workers, batch sizes or startup work, and avoid loading a full LLM into a small container. Ask the Technical Lead before any resource upgrade. |
| Sleeping or suspended application | Check the account's documented lifecycle, expiry and quotas. Follow the supported recovery route or contact the Technical Lead; do not assume retries create extra quota. |

Do not delete shared data, disable security or invent CLI flags/error-code
workarounds to clear a deployment failure.

## 12. Resource and trial limitations

**Account/workspace entitlements must be confirmed.** Trial eligibility,
duration, resource limits, managed services and any credits depend on the
assigned allocation. Public plan examples do not promise identical resources
for every participant, free upgrades or unapproved paid infrastructure.

The Organising Committee should communicate event-provided accounts or
workspaces, credits, allocated services, relevant limits and assessment-access
arrangements. See the official
[limits and lifecycle reference](https://primecloud.cloud/docs/limits).

Keep the application accessible during the scheduled assessment. Trial
environments may sleep after inactivity: open and verify the assigned URL
shortly before judging and follow the documented lifecycle if it has slept.
Check expiry/suspension as well. Do not promise continuous availability,
conceal an unavailable service or purchase an upgrade without approval.

## 13. Submission checklist

- Assigned PrimeCloud HTTPS application URL and `GET /healthz` URL.
- API/sync/workflow path and safe example requests or interaction steps.
- GitHub repository, selected challenge and deployed commit/revision.
- Sanitized deployment-status evidence, useful deployed-application
  screenshots and hosted functional test results.
- README with actual build/start commands, runtime/port configuration,
  environment-variable names, storage/model setup and known limitations.
- Integrated DSA source, complexity explanation and required test/comparison
  evidence from the challenge card.
- The common 2-3 minute backup demo video and team/contribution/SDG
  information required by the [General Rules](../../general-rules.md).

Do not submit passwords, tokens, private keys or raw secret configuration.
No custom domain, separate slide deck or formal Track-Level presentation is
required. A backup video does not replace the mandatory hosted application.

## Related guidance

- [Software Development overview](index.md)
- [Challenges and acceptance criteria](challenges.md)
- [Track rules and assessment](rules.md)
- [PrimeCloud platform](https://primecloud.cloud/)
- [Official documentation](https://primecloud.cloud/docs)
- [Official quickstart](https://primecloud.cloud/docs/quickstart)
- [Application deployment and runtime](https://primecloud.cloud/docs/applications)
- [Configuration](https://primecloud.cloud/docs/configuration)
- [Security and secrets](https://primecloud.cloud/docs/security)
- [Databases](https://primecloud.cloud/docs/databases)
- [Storage](https://primecloud.cloud/docs/storage)
- [Troubleshooting](https://primecloud.cloud/docs/guides#troubleshooting-doctor)
- [Limits and lifecycle](https://primecloud.cloud/docs/limits)
