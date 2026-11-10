---
name: file-delivery
description: "Serve stored files without passing their bytes through the app server: public CDN URLs, a Worker for access-controlled files, and redirects for downloads. Load before adding or changing any route, view, or job that serves, downloads, previews, frames, or reads stored files."
---

# File Delivery

App servers never carry stored file bytes to a browser. The browser fetches
the file from storage's CDN. The app server checks access, counts, and signs,
then hands off.

## Rationale

On 2026-11-10 a 5.8 MB revealjs deck on academic.page took 14-21 seconds to
appear. PHP fetched it from Cloudflare R2 and relayed it on every view. From
the Hetzner servers, R2's S3 API endpoint
(`<account>.r2.cloudflarestorage.com`) ran at 0.2-0.5 MB/s on pequod's box
and 0.5-1.9 MB/s on framework.pub's box. The bucket's public domain ran at
9-17 MB/s from the same box. A relay also holds a PHP worker for the whole
transfer.

## Delivery model

| File | Delivery |
|---|---|
| Public file | The bucket's public CDN domain, such as `media.academic.page`. |
| Access-controlled file | A Cloudflare Worker with an R2 binding. The Worker checks the app's signed token and streams the object from R2 inside Cloudflare. |
| Download | The app records the download, then answers 302 to a short-lived link that sets `Content-Disposition: attachment; filename=...`. The link is a presigned URL with `response-content-disposition`, or the Worker's signed URL where a Worker exists. |
| Embedded HTML (decks, notebooks, reports) | An iframe whose `src` is the CDN or Worker URL, isolated by the iframe's `sandbox` attribute. Headers come from the Worker or a Cloudflare rule. |
| Short link or tracked link | The app counts, then answers 302. |

## Rules

- Never put a stored file in a response body. `response()->stream`,
  `streamDownload`, `fpassthru`, `Storage::get` returned as content,
  `$disk->response`, and `$disk->download` are relays. Replace each with a
  redirect or a direct URL.
- Do per-file changes once, at upload or publish time, or in the Worker.
  Examples are header injection, link rewriting, previews, chart specs, and
  zip archives. Store the result in the bucket and serve it like any other
  file.
- Count views on the page that embeds the file, or with a beacon. Count
  downloads in the redirecting route before the 302.
- A server-side read for processing (conversion, import, mirroring) is
  allowed. On these servers, read a public bucket through its public domain
  rather than the S3 API, with a unique query string so Cloudflare's cache
  never answers. Fall back to the S3 API when the public read fails.
- Generated content that is not a stored file (a BibTeX export, a demo
  fixture) may come from the app.

## Project notes

- **academic.page (pequod):** every object in the `pequod` bucket is public at
  `media.academic.page`. `App\Support\MediaReader` does processing reads.
- **framework.pub:** artifacts can be private or password-protected and
  include bundles with relative asset paths. The `framework-content` Worker
  serves them on `content.framework.pub/c/*`, from links the app signs with
  `App\Support\ContentWorker` (live 2026-11-10). Downloads go through the
  same Worker.

## Review check

Before finishing work that touches files, search the diff for the relay calls
listed under Rules. Every hit needs a redirect, a direct URL, or a note that
it is generated content.
