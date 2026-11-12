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

This guide covers the initial participant workflow. Use the
[official PrimeCloud documentation](https://primecloud.cloud/docs) and
[quickstart](https://primecloud.cloud/docs/quickstart) as the platform source
of truth. Follow their current console instructions if labels or procedures
change. The steps below are not a new PrimeCloud CLI specification.

## 1. Prerequisites and access

Before deploying, prepare:

- A PrimeCloud account/workspace and permission to deploy in the assigned
  project/environment, confirmed through the organizer's approved access route.
- Your team's GitHub repository, chosen branch and known working commit.
- The project's dependency manifest/lockfile, runtime requirements and actual
  build/start instructions.
- A locally working application with an HTTP interface and `GET /healthz`.
- Non-sensitive sample inputs and expected outputs for your selected challenge.
- For B, an organizer-approved persistent remote database/storage arrangement.
- For C, approved inference access reachable from the hosted application.

Confirm available resources, trial eligibility/expiry, service permissions,
storage and any costs with the Technical Lead before provisioning. Public
plan examples are not event entitlements. Do not assume unlimited credits,
always-on availability, a particular database allocation or shared API keys.
Do not incur unapproved charges.

Raise missing access or dependencies early. Record the issue, but do not
substitute a local-only run for successful mandatory deployment.

## 2. Prepare the application for hosting

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

PrimeCloud documents detection of Dockerfiles, Procfiles and supported package
manifests. Use your actual project's supported format; you are not required
to add every format or install a CLI. If repository authorization is
unavailable, ask the Technical Lead to confirm a supported deployment route.

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

## 6. Provide health checks

Implement **`GET /healthz`** and configure the deployment's health-check path
through the documented platform settings.

The endpoint should respond quickly, use appropriate status codes and expose
no secrets, credentials or sensitive diagnostic details. Explain what it
checks and distinguish process health from dependency readiness where
relevant. Avoid expensive model generation or a full dataset reconciliation
on every probe.

A successful health check proves neither the DSA implementation nor the core
workflow. Both require the separate functional verification below.

## 7. Environment variables and secrets

Document required **variable names and purposes**, not real values. Configure
runtime settings using PrimeCloud's documented application/environment
controls. Its official documentation describes Vault-backed secret bindings;
use the supported secret-management/binding route for credentials.

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

**Challenges A and C:** explain whether results, uploaded files or the
knowledge base are persisted, supplied with the deployment or rebuilt.
Reproducible stateless processing is acceptable where it meets the challenge;
do not claim durability for ephemeral files. Use only permitted, non-sensitive
documents and records.

Avoid destructive resets of shared services. Any restart/redeployment or
storage test must remain within your assigned resources and permissions.

## 9. Deploy and verify

1. Start deployment through the documented Console workflow.
2. Inspect build and runtime logs. Resolve configuration, startup, port or
   dependency failures.
3. Open the **assigned PrimeCloud HTTPS URL** and verify `GET /healthz`.
   Check from a browser/session independent of your local development server.
4. Execute the actual challenge workflow through the hosted service, using
   known sample inputs and checking expected against observed outputs.
5. Run the relevant failure/edge scenarios and preserve sanitized evidence.
6. Record the deployed revision, test time, URL and any limitations.

| Challenge | Minimum hosted verification |
|---|---|
| A | Submit examples in two supported formats; inspect actual reconciled records, matching results and ambiguous review items/decisions. Verify invalid-input reporting. |
| B | Load the hosted interface, work online, go offline, create/edit/delete and reload, reconnect and sync. Show two-session conflicts, retry/lost-acknowledgment deduplication and remote persistence across a permitted restart/redeployment. |
| C | Use permitted documents or the supplied knowledge base; demonstrate heap-selected evidence, a grounded cited result, missing-evidence behavior and explicit service-error handling. |

If the approved plan sleeps or expires, follow its documented lifecycle and
confirm how the app will be available for assessment. Do not promise
continuous availability or hide an unavailable deployment.

## 10. Submission checklist

- Assigned PrimeCloud HTTPS application URL and `GET /healthz` URL.
- API/sync/workflow path and safe example requests or interaction steps.
- GitHub repository, selected challenge and deployed commit/revision.
- Sanitized deployment-status evidence and hosted functional test results.
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
