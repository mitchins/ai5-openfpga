# Licensing and redistribution

Status: **pre-import license audit**, 6 November 2026. This repository's source code and
release packaging still need an exact, pinned-dependency audit after the port is imported.
This document records what was verified, which rights are separate, and what must not
be published. It is not a substitute for a legal opinion.

## Application code: GPL-3.0-or-later

Project-authored code intended to form part of the combined AI5/openfpgaOS application
is licensed under **GPL-3.0-or-later** (root [LICENSE](LICENSE)). This is a
project license choice, **not** a claim to relicense other authors' standalone works.

The relevant upstream code grants permission to use GPL version 2 **or any later
version**, despite GitHub's abbreviated "GPL-2.0" repository labels:

- [nunuhara/ai5-sdl2](https://github.com/nunuhara/ai5-sdl2):
  see e.g. [src/vm.c](https://github.com/nunuhara/ai5-sdl2/blob/master/src/vm.c),
  [src/main.c](https://github.com/nunuhara/ai5-sdl2/blob/master/src/main.c).
- [nunuhara/libai5](https://github.com/nunuhara/libai5):
  see [src/mes/parse.c](https://github.com/nunuhara/libai5/blob/master/src/mes/parse.c).
- [nunuhara/nulib](https://github.com/nunuhara/nulib):
  see [src/buffer.c](https://github.com/nunuhara/nulib/blob/master/src/buffer.c).

An inspection of 127 `.c` / `.h` files on the three upstream default branches
found 117 explicitly GPL-2.0-or-later files, six MIT/BSD files, two BSD-3-clause
`inih` files, one public-domain `sts_mixer.h`, and one unmarked character mapping
table (`nulib/src/s2utbl.h`). There were **no GPL-2.0-only declarations** in
this inspected code. The unmarked table's origin, any future/upstream changes,
and the actual **pinned revisions imported into this repository** must still be
verified. Preserve individual copyright/license notices, including in third-party
headers and font bundles.

## SDK compatibility: resolved for the application code

The openfpgaOS SDK at the originally qualified commit
[`a408ddc12aed0dfaa4aa22c06af82f829db77126`](https://github.com/openfpgaOS/openfpgaSDK/tree/a408ddc12aed0dfaa4aa22c06af82f829db77126)
declares **Apache-2.0** for SDK-authored files, including
[`src/sdk/of_sdl2.c`](https://github.com/openfpgaOS/openfpgaSDK/blob/a408ddc12aed0dfaa4aa22c06af82f829db77126/src/sdk/of_sdl2.c).

Apache-2.0 is compatible with **GPLv3**, but not GPLv2-only:
[GNU](https://www.gnu.org/licenses/license-list.en.html#apache2),
[Apache Software Foundation](https://www.apache.org/licenses/GPL-compatibility).
The upstream AI5 sources' express "or later" grant allows the combined
AI5 + Apache-2.0 SDK application to be distributed under GPLv3 terms,
**subject to all actually linked components and their notices being checked**.
Do not describe this combined executable as GPLv2-only or Apache-2.0-only.

For distributed GPL executables, provide the complete corresponding source,
local changes, build/install scripts, dependency pins, and required notices.

## Separate Pocket runtime and FPGA bitstream: distribution check required

The SDK's pinned [NOTICE](https://github.com/openfpgaOS/openfpgaSDK/blob/a408ddc12aed0dfaa4aa22c06af82f829db77126/NOTICE)
identifies `os.bin` and `*.rbf_r` as generated runtime artifacts whose FPGA
bitstream includes more than Apache-2.0 code. The upstream openfpgaOS
[NOTICE](https://github.com/openfpgaOS/openfpgaCore/blob/main/NOTICE)
and [REUSE.toml](https://github.com/openfpgaOS/openfpgaCore/blob/main/REUSE.toml)
identify:

- Analogue's proprietary Pocket Framework under its own APF agreement and EULA;
- Intel/Altera megafunction IP with device-use restrictions;
- MiSTer-derived Analogizer video RTL with GPL obligations;
- other components with their own notices.

Analogue's [developer packaging documentation](https://www.analogue.co/developer/docs/openfpga/getting-started)
contemplates distributing compiled Pocket cores, but **that does not make
all bundled source/media Apache-licensed or remove third-party terms**.

**Release condition:** before publishing an installable binary ZIP, document
the exact bitstream/`os.bin` provenance and applicable permissions/notices,
and obtain clarification from upstream maintainers if those terms remain
unclear. Merely using SDK output is not proof of unrestricted redistribution.
Do not publish private development or game-containing ZIPs.

## Data, fonts, and audio

- **Original game files:** Do not commit, package into a public release,
  upload, or link to original archives, graphics, scripts, music, dialogue,
  extracted/converted data (`A5PK`), or captures. A public release must require
  users to supply their own legally obtained compatible data.
- **Sound bank:** The SDK's [SoundFont notice](https://github.com/openfpgaOS/openfpgaSDK/blob/a408ddc12aed0dfaa4aa22c06af82f829db77126/LICENSES/LicenseRef-Proprietary-SampleData.txt)
  identifies `bank.ofsf`/SC-55 samples derived from Roland ROM material
  with no confirmed redistributable license. **Exclude from public assets**
  unless permission is documented or replace with an appropriately licensed bank.
- **Fonts:** Upstream AI5-SDL2 includes DotGothic16 and NotoSansJP with SIL OFL
  notices and Kosugi with Apache-2.0 terms. Preserve accompanying license files
  when distributing. `fonts/wine_tahoma.ttf` has no adjacent license file in
  that repository; exclude it from public packaging until its provenance and
  redistribution terms are established.
- **Fixtures:** Use wholly synthetic or independently licensed fixtures in CI.
  Keep tests involving original game data local, opt-in, and outside Git.

## Public release gates

1. Import source with traceable upstream commit IDs, local changes and original
   copyright notices. Re-check the **exact pinned** engine, libai5, nulib,
   SDK and other linked inputs for license compatibility.
2. Run a clean source build and all asset-free tests; retain reproducible
   build scripts and source corresponding to any distributed ELF.
3. Assemble a **public** ZIP separately from private SD-card test packages.
   Reject original-game file patterns, private A5PKs, unapproved fonts,
   `*.ofsf` banks and game captures. Review the final ZIP manifest,
   not merely `.gitignore`.
4. Satisfy and record runtime/bitstream distribution terms and notices before
   publishing `*.rbf_r` or `os.bin` artifacts.
5. Keep the project's public compatibility and hardware-test statements tied
   to actual qualified evidence.

**Current decision:** public source preparation can proceed on a GPLv3-or-later
basis. A public downloadable *playable* binary release is on **HOLD** until
the exact linked-dependency audit and separate runtime/media gates above pass.
