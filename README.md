# AI5 for openFPGA

Experimental port of the [AI5-SDL2](https://github.com/nunuhara/ai5-sdl2) visual-novel engine to the [openfpgaOS](https://github.com/openfpgaOS) SDL/RISC-V environment for the Analogue Pocket.

**Status:** source import and device qualification are in progress. This repository is not yet a public, playable release. Desktop qualification of specific Dōkyūsei (1999) routes does **not** establish full game compatibility or execution on Pocket hardware.

## Licensing

See **[LICENSING.md](LICENSING.md)** before importing source, distributing an ELF, or creating a Pocket SD-card release.

- The combined application is intended to be distributed as **GPL-3.0-or-later**; the original AI5, libai5, and nulib source headers allow GPL version 2 **or later**, which is compatible with the SDK's Apache-2.0 code when distributing the combined application under GPLv3 terms.
- Preserve upstream copyright, license, and font notices. Verify the exact imported revisions and linked dependencies.
- **Do not commit or distribute original game data** (including extracted or converted A5PK archives), proprietary audio samples, or unlicensed fonts.
- **Do not publish the private test SD-card ZIP.** Its game content and bundled runtime are not automatically cleared for redistribution.
- Public redistribution of an openfpgaOS runtime/FPGA bitstream requires a separate provenance and license check. The SDK's SC-55-derived `bank.ofsf` is specifically excluded unless rights are established.

Public source preparation is permitted. A downloadable playable package remains on **hold** until the gates in [LICENSING.md](LICENSING.md) are satisfied.

## Upstream projects

- [nunuhara/ai5-sdl2](https://github.com/nunuhara/ai5-sdl2)
- [nunuhara/libai5](https://github.com/nunuhara/libai5)
- [nunuhara/nulib](https://github.com/nunuhara/nulib)
- [openfpgaOS/openfpgaSDK](https://github.com/openfpgaOS/openfpgaSDK)

This is an independent community port, not an official Analogue or game-publisher release.
