# macOS Internals Lab

A small, free, GitHub Actions–based lab for hands-on practice with macOS security internals — built for interview prep on detection engineering and OS internals (Gatekeeper, TCC, SIP, launchd persistence, and unified logging).

Runs entirely on GitHub's free, unlimited macOS runners for public repositories — no local Mac, no cloud VM rental, no cost.

## What's inside

- `.github/workflows/macos-test.yml` — a manually-triggered workflow that runs a series of real commands against a live Apple Silicon macOS runner and prints the output to the Actions log.

## How to run it

1. Go to the **Actions** tab of this repo.
2. Select **macOS Internals Lab — Full** from the left sidebar.
3. Click **Run workflow**.
4. Once it finishes, click into the run to see each step's output.

No setup required beyond having the workflow file in the repo — GitHub provisions a fresh macOS runner for each run and tears it down afterward.

## What each section demonstrates

| Section | Concept | What it shows |
|---|---|---|
| OS baseline | Environment | macOS version, architecture, and hardware model of the runner |
| SIP | System Integrity Protection | Whether SIP is enabled and which specific protections are active |
| Gatekeeper | Code execution trust | Gatekeeper's assessment of a real signed system app, plus the underlying code-signature details it checks |
| TCC | Privacy/permission control | Confirms SIP protects the TCC database even from the runner's own user — a direct query is expected to fail |
| launchd persistence | Startup mechanisms | Enumerates existing LaunchAgents/LaunchDaemons, then writes, loads, and cleans up a test LaunchAgent to show the full persistence lifecycle |
| Unified logging | Telemetry | Pulls a real log snapshot and runs a predicate-filtered query scoped to launchd activity |
| Endpoint Security (ESF) | EDR-level telemetry | Attempts `eslogger`, expected to fail without Full Disk Access/entitlements — the same restriction real EDR agents must be granted |
| Mini detection | Detection engineering | A tiny example of writing a log query that flags a specific behavior (a LaunchAgent load event) — detection logic in miniature |

## Why the failures matter

A few steps (the TCC.db query, `eslogger`) are *expected* to fail on a stock CI runner. That failure is the point — it's hands-on proof of exactly how SIP and Apple's entitlement model restrict access, which is a stronger thing to describe in an interview than reciting the concept from memory.

## Cost

$0. GitHub Actions macOS runners are free and unlimited on public repositories.
