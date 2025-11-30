## *OpenSource product!*
# SUPPORTED ONLY CORE LINUX
[EN]
# How use?
- For start download package manager https://bun.com/ [BUN]
```bash
git clone https://github.com:GitZipQR-vault/GitZipQR.app.git
cd GitZipQR.app
bun install
git clone https://github.com/GitZipQR-vault/GitZip.cpp 
git clone https://github.com/GitZipQR-vault/PaperStorageX
./rub.sh 
```
[RU]
Как использовать?:
- Для начала скачиваем пакетный менеджер https://bun.com/ [BUN]
- Введите в терминал 
```bash
git clone https://github.com/GitZipQR-vault/GitZipQR.app.git
cd GitZipQR.app
bun install
git clone https://github.com/GitZipQR-vault/GitZip.cpp 
git clone https://github.com/GitZipQR-vault/PaperStorageX
./run.sh
```
**Core idea:** ship a hardened UI around your existing C++ binaries (`encode`/`decode`), add A4 PDF packing, Live Scan, and a licensing check via ETH/USDT on your address. This repo avoids touching your C++ core.

## Features
- Runs your binaries for Encode/Decode.
- Packs PNG chunks into A4 PDF (3x3 grid).
- Live Scan: assemble chunks from a line-feed barcode scanner.
- License: machine fingerprint + payment check (USDT>=1500 or ETH>=0.5).
- Hardening: `asar`, minification, JS obfuscation, optional AES-GCM layer for a bootstrap file.

> No protection is absolute. Keys live in memory at runtime. This stack raises attacker cost.

## Dev
1. Copy `.env.example` to `.env`, set:
   - `ETH_RPC`
   - `BIN_ENC` / `BIN_DEC` (your built C++ binaries)
2. `./start-dev.sh`

## Build
- Linux AppImage: `bun run dist:linux`
- Windows NSIS .exe: `bun run dist:win`

Artifacts are placed in `packages/app/release/`.

## Commands
- `bun run dev` — run Next (UI) + Electron.
- `bun run pack-a4 <dir> <out.pdf>` — build A4 sheets.
- `bun run scan-live` — collect chunks from scanner (stdin).

## Notes on hardening
- `electron-builder` with `asar: true`.
- `javascript-obfuscator` passes: control-flow, dead-code, string-array, debug-protection.
- Optional AES-GCM: decrypt a small bootstrap at runtime with a key derived from machineHash + secret.
- Consider code signing and a commercial native protector for Windows if you need more (VM-based).
