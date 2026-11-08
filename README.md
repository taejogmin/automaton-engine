# automaton-engine

The chess engine used by **Automaton** (a chess game in IRIS on [haveaseat.net](https://haveaseat.net)), published here so anyone can get its complete corresponding source under the GNU General Public License v3.

Automaton runs this engine in the player's browser (in a Web Worker). The engine is a separate program that talks to the game only through UCI text messages. This repository covers only the engine. The rest of the site is not part of it.

## What is served

| File served by haveaseat.net | SHA-256 |
|---|---|
| [`dist/stockfish-19-lite-single.js`](dist/stockfish-19-lite-single.js) | `ccb130d7ff29408531c47d859a49f91d59d4f482d05a53eb1a3231a4f624c91a` |
| [`dist/stockfish-19-lite-single.wasm`](dist/stockfish-19-lite-single.wasm) | `ee4f115bdb2d32cadf96cada104a05b5ec257d7ad6f57582190b49bc71f096de` |

These are the unmodified `bin/stockfish-19-lite-single.*` files from the npm package [`stockfish@19.0.1`](https://www.npmjs.com/package/stockfish/v/19.0.1). That package is Stockfish.js by Nathan Rugg and contributors, a WebAssembly build of [Stockfish](https://stockfishchess.org) 19. We have made **no changes**.

## Corresponding source

- [`upstream/`](upstream/) is the full source tree of [nmrugg/stockfish.js](https://github.com/nmrugg/stockfish.js) at tag `v19.0.1`, commit `0d5dd7944f88c817c07a26bc4fb1905d5f9c46d6`, copied unmodified. It contains the Stockfish C++ source, the Emscripten glue, and the build script.
- [`nets/nn-61e7af4bb97d.nnue`](nets/) is the "lite" neural network embedded in the lite builds (`EvalFileLiteName` in `upstream/src/evaluate.h`). Its SHA-256 starts with `61e7af4bb97d`, as the file name requires.

## Building

1. Install [Emscripten](https://emscripten.org) `6.0.9`. This is the version `upstream/build.js` checks for.
2. Put the network file where the build expects it:
   ```sh
   cp nets/nn-61e7af4bb97d.nnue upstream/src/
   ```
3. Build the single-threaded lite flavor:
   ```sh
   cd upstream
   node build.js --single-threaded --lite
   ```
   The output is `upstream/src/stockfish-19-lite-single.js` and `.wasm`. Run `node build.js --help` to see every option.

## Versions

| Date | Engine | Used by |
|---|---|---|
| 2026-11-08 | Stockfish.js 19.0.1 (Stockfish 19), lite single-threaded | Automaton (first version) |

When the site moves to a new engine version, this repository is updated in the same release. Each version is tagged, for example `v19.0.1`.

## License

The engine is GNU GPL v3. See [`LICENSE`](LICENSE), which is the same text as `upstream/Copying.txt`. The credits are in [`upstream/AUTHORS`](upstream/AUTHORS) and [`upstream/README.md`](upstream/README.md).

---

**한국어 안내:** 이 저장소는 Have a Seat의 체스 게임 Automaton이 브라우저에서 쓰는 Stockfish 엔진의 원본 소스입니다. GPLv3에 따라 공개합니다. 엔진은 고치지 않고 그대로 씁니다. 빌드 방법과 정확한 버전은 위 영어 안내에 있습니다.
