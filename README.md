# vocoder-juce

Compilation must be done either in Linux or in WSL.

## Setup JUCE_emscripten

`git clone https://github.com/Dreamtonics/juce_emscripten.git`

### Subtle changes to juce_emscripten

If compiling in WSL, make sure the following changes are made to the juce_empscripten module code.

#### juce_emscripten/modules/juce_product_unlocking/marketplace/juce_OnlineUnlockStatus.cpp

```cpp
// line 282
#elif JUCE_LINUX || JUCE_EMSCRIPTEN
```

#### juce_emscripten/modules/juce_core/native/juce_BasicNativeHeaders.h

```cpp
// copy and paste the section under `#elif JUCE_LINUX || JUCE_EMSCRIPTEN` including that line
// remove `|| JUCE_EMSCRIPTEN` from the original and remove `JUCE_LINUX ||` from the copy
// then remove the following includes:
#include <sys/prctl.h>
#include <sys/ptrace.h>
```

# Setup instructions

## Setup Clang (if missing)
https://ubuntuhandbook.org/index.php/2023/09/how-to-install-clang-17-or-16-in-ubuntu-22-04-20-04/

## Setup Emscripten

Instructions to setup Emscripten environment can be found here: https://emscripten.org/docs/getting_started/downloads.html.

Follow the Linux setup instructions. If using WSL, the same instructions apply.

## Compiling with Emscripten

- Do not use JUCE_emscripten's or the offical JUCE repo's version of Projucer to resave the Emscripten build target! Instead, build and run Projucer from our forked [JUCE-emmake](https://github.com/CS-3311-JDE-3346/JUCE-emmake) repo
- Navigate to the Emscripten build target directory
- `cd Builds/Emscripten`
- Run emmake on the makefile
- `emmake make`
- If using in another project, make sure to copy `vocoder.js`, `vocoder.wasm`, and `vocoder.data` to the same folder

# Using

- C++
- JUCE Framework
- [Voclib](https://github.com/blastbay/voclib/tree/master)

# Reasoning

The first MVP we targetted was getting basic functionality of the vocoder. The reasoning we chose this as our first MVP was because we need to have basic functionality before we try to add aditional features, as the additional features build off the basic functionality.
