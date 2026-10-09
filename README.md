# TypeScript for Deck

`typescript-language-server`, for `.ts` and `.tsx`. A project is anything with a `tsconfig.json`.

```sh
npm i -g typescript-language-server typescript
```

Both are needed: the server is a wrapper around the compiler, not a replacement for it.

The JavaScript definition names the same `serverId`, so one server session serves both languages
in a project that mixes them rather than two processes analysing the same files.

## Debugging

**Debug <file>.ts** in the editor's Run and Debug panel (or F5) runs the file under Node with
breakpoints, stepping and variables. It needs **js-debug**, the debugger VS Code uses, which is a
separate download. **Settings -> Plugins -> Languages** says whether it was found, and its
**Install** button downloads it from the vscode-js-debug releases, checks it against the SHA-256 in
`language.json`, and unpacks it into `%LOCALAPPDATA%\Deck-tools\js-debug`. The Run and Debug panel
offers the same button when the debugger does not start.

By hand: unpack `js-debug-dap-v1.140.0.tar.gz` from
https://github.com/microsoft/vscode-js-debug/releases into that folder, so that
`%LOCALAPPDATA%\Deck-tools\js-debug\js-debug\src\dapDebugServer.js` exists.

Node.js must be on PATH. The language server installs from the same panel
(`npm install -g typescript-language-server typescript`).

TypeScript runs as Node runs it, by stripping the types, which needs Node 23.6 or later. A
`.tsx` file cannot be run that way.

## Installing it

From inside Deck: **Settings -> Plugins -> Browse**, pick it, and it loads straight away.

By hand: copy this folder into `%APPDATA%\Deck\languages\` (`Deck-Dev` for a debug build).
`docs/languages.md` in the Deck repository documents the format.

## What a definition can and cannot do

It is **data**, not code. `language.json` is parsed field by field and never executed, which is
why a language is a different kind of thing from a plugin even though both are folders Deck
reads at startup. The worst a malformed one can do is skip itself.
