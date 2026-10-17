---
title: Workflow
tags: [howto]
updated: 2026-10-15
---

# Workflow

## Edit

The game is one file with long lines. Grep by function name (see [Architecture](Architecture.md)) and edit with a script or a targeted replace; never retype large regions from memory. Back the file up before a patch. Syntax-check all script blocks after editing:

```bash
node -e "const s=require('fs').readFileSync('netmancer.html','utf8');const re=/<script>([\s\S]*?)<\/script>/g;let m;while((m=re.exec(s))){try{new Function(m[1])}catch(e){console.log('SYNTAX',e.message)}}"
```

## Test

The built-in browser pane cannot open `file://`, so serve the folder:

```bash
node -e "require('http').createServer((q,r)=>{const p=decodeURIComponent(q.url.split('?')[0]);require('fs').readFile('.'+(p==='/'?'/netmancer.html':p),(e,d)=>{if(e){r.writeHead(404);return r.end()}r.writeHead(200,{'Content-Type':p.endsWith('.html')?'text/html; charset=utf-8':'text/plain','Cache-Control':'no-store'});r.end(d)})}).listen(8765,'127.0.0.1')"
```

Then open `http://127.0.0.1:8765/netmancer.html#selftest`. The page runs four suites and prints a report (`#devreport`): engine (`C.selfTest`, which includes the lab API and a replay of every course lesson), workstation (`uiSelfTest`), game modes (`modeSelfTest`) and lab and course (`labSelfTest`). All four must say PASS. In normal play the same report is under Settings → Diagnostics.

Demo hashes for screenshots: `#demo-mail` (desktop, a VPN bad ticket open), `#demo-phone` (same at phone size), `#demo-academy` (an Academy ticket). Dev modes use a throwaway save.

Phone checks: 390×844, no horizontal scroll, tap targets ≥ 44 px.

## Publish

The playable copy at https://claude.ai/artifact/WGEWFFJycGFEWpFZ8CEwDK is the same file with the `<!DOCTYPE>`, `<html>`, `<head>` and `<body>` wrappers stripped, the charset and viewport metas removed, and `<title>Netmancer</title>`. Build that copy into a scratch file and publish it with the Artifact tool against that URL.

## Commit

Commit in `E:\Projects\Netmancer` only. After a change: update the relevant page here, add a line to the [Backlog](Backlog.md) *Done* list if it closes an item, and add a [session note](Sessions/).

## Publish to the web

The repo's `main` branch is served by GitHub Pages at https://cdsweeney2016.github.io/netmancer/ (`index.html` opens `netmancer.html`). Pushing to `main` publishes; the build takes a minute or two. Testers' saves live in their own browsers. The claude.ai artifact is a separate, private copy republished by hand.
