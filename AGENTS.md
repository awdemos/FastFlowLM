# FastFlowLM

## OVERVIEW

NPU-first runtime for AMD Ryzen™ AI (XDNA2 NPUs). Ships a lightweight CLI and local server that run LLMs, VLMs, and embedding models on the NPU without a discrete GPU.

## STRUCTURE

```
src/              C++ runtime, CMake build, runner/server, NPU backends (XRT / HRX)
docs/             Jekyll site and Linux getting-started guide
debian/           Debian packaging files
hrx-integration/  HRX runtime fetch scripts
assets/           Logo and demo assets
bench_config.json Benchmark configuration
```

## COMMANDS

Build (Windows, with Visual Studio):
```bash
cd src
make all          # cmake --preset windows-vs18, then build
make run          # run llama3.2:1b in the out/ directory
make serve        # serve qwen2.5vl-it with 32k context
make clean
```

Linux build:
```bash
cd src
mkdir -p build
cmake -S . -B build -DFLM_VERSION=1.0.0 -DNPU_VERSION=1.0
cmake --build build --parallel
```

Runtime CLI:
```powershell
flm run llama3.2:1b
flm serve llama3.2:1b
flm list
flm pull llama3.2:1b --force
```

## SETUP

- Windows: install the MSI from releases; requires AMD NPU driver 32.0.203.311+.
- Linux: follow `docs/linux-getting-started.md` or use the `docs/setup.sh` helper.
- Models download from HuggingFace automatically; set `FLM_MODEL_PATH` to override the default model directory.
- Disable the startup version check with `FLM_DISABLE_UPDATE_CHECK=1`.

## CODE STYLE

- C++20
- CMake minimum 3.22
- Run `make` from `src/`; do not commit `build/` or `out/`.

## DEPLOYMENT

No Dagger module or recognized deployment configuration was found. The packaged installer is the primary distribution.
