---
name: project-tunnels
description: "Load whenever doing web application work to prepare, verify, and share the project's HTTPS tunnel URL. Also use when creating or troubleshooting project or worktree previews on the Mac or remote-code. Share tunnel links instead of Herd .test or localhost links."
---

# Project tunnels

When doing web application work, include the exact checkout's HTTPS tunnel URL
in preview updates and the final handoff. Use this URL as the user-facing link.
Herd `.test` and localhost addresses are local origin details. Preserve this
preference and the discovered URL in existing project context or agent handoffs.
If the preview is blocked, report the blocker and what was verified rather than
presenting an unverified URL as ready.

## Discover the correct URL

On the Mac, run `tunnels` or `~/System/config/bin/tunnels`. Match its path to the
checkout being edited, especially for worktrees. `tunnels -a` includes other
Herd proxies. A main checkout's URL does not preview a separate worktree.

The shared tunnel already runs at login. Registering a local site makes it
available through that tunnel; do not create a separate Cloudflare tunnel for
each project. These mappings explain the routing, but discover the exact URL
instead of guessing:

- `<site>.test` maps to `https://<site>.pequod.dev`.
- `<sub>.<site>.test` maps to `https://<sub>--<site>.pequod.dev`.
- Names reserved for real public sites use `<site>-mac.pequod.dev` on the Mac.
  For example, the local Flint project uses `https://flint-mac.pequod.dev`.
- VM previews have their own registered names, such as `fc-<worktree>`.

## Prepare a project or worktree

Use the project's registered T3 **Workspace setup** script or documented setup
command first. It may also prepare dependencies, databases, and environment
files. Inspect existing registrations before creating one so a preview keeps
pointing to its intended checkout.

For registered Herd worktrees, prefer the setup script, then the managed wrapper:

```text
projectctl workspace-herd-link <alias> <domain> <absolute-workspace-path> [--isolate <php-version>] [--secure]
```

The wrapper manages checkout environment files and isolated databases. Its
matching cleanup command is `projectctl workspace-herd-unlink <alias> <domain>
[--keep-databases]`; follow the project's worktree lifecycle for cleanup.

For a simple unregistered Herd site, run `herd link <unique-site-name>` from the
exact checkout directory. Use a unique name for each worktree. Keep the
project's required PHP version and HTTPS setup. Then rerun `tunnels`.

Registered main Herd projects use `projectctl bootstrap <alias>` for initial
setup. This prepares dependencies and databases; do not run it just to discover
a URL.

Container workspaces use the project's setup command or
`projectctl workspace-link <alias> <domain.test> <absolute-workspace-path>`.
This requires `docker-compose.yml` and configured project metadata and runtime.
It publishes through Herd proxy on a Herd Mac and Caddy on Caddy machines.
Use exact unique hostnames; wildcard container previews are unsupported on
Herd. Main container projects use their registered `projectctl up <alias>` flow.
Check project instructions for dependencies and readiness.

Shared configuration for an entirely new project belongs in
`~/System/config/projects/projects.yml` and Ansible. Follow `system-config`
for these changes. Do not invent app ports or install new infrastructure.

On remote-code, use its registered workspace setup script and run
`~/.local/bin/preview-route list` there for exact VM URLs. Its routing is managed
by the infra repository, documented in `directions/remote-code.md`.

For Quarto previews, run `quarto-preview <doc.qmd>`, check
`quarto-preview status`, and use the project's tunnel URL from `tunnels` with
the `/preview` route.

## Make the preview usable remotely

Build frontend assets using the project's build command. A Vite dev server
referenced through localhost only works on the Mac. Check for stale hot-file
references if the public page still requests localhost assets, following the
project's workflow for switching to built assets.

Configure the application's trusted proxies as appropriate for the local
loopback proxy so it honors the forwarded HTTPS host. Generated links,
redirects, and asset URLs must stay on the public host. Follow project-specific
authentication and callback settings where needed.

Verify the local origin serves the intended checkout and inspect public routing
before reporting readiness. A Cloudflare Access login redirect confirms the
Access gate responds; it does not verify the application behind it. State that
limit if an authenticated public check is unavailable. When browser verification
is requested, inspect the public page and its assets after authentication.

Share a clickable HTTPS tunnel link, including the relevant route when useful,
and briefly state what was verified. Cloudflare Access supports Erik's GitHub
login or emailed PIN. Leave Access enabled.

## Troubleshoot shared routing

Read `~/System/AGENTS.md` (Sharing preview links) and the preview-routing section
of `~/System/README.md` for the current Mac configuration. Check the services
with `launchctl print gui/$(id -u)/com.erik.system.preview-caddy` and
`launchctl print gui/$(id -u)/com.erik.system.preview-tunnel`. Logs are
`~/.config/preview-route/caddy.log` and
`~/.config/preview-route/cloudflared.log`.

On remote-code, routing uses Caddy and `remote-code-previews.service`.
Infrastructure failures belong in the owning System or infra repository.
Load `system-config` before changing Mac configuration, contact an active
mac-system agent when available, and reconcile changes through Ansible.
Keep tunnel credentials private and preserve the Access policy.
