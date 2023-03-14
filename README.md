how to run llama.cpp on windows
-------------

I'm not familiar with windows development, here are just something I wish can help.

please refer to [llama.cpp](https://github.com/ggerganov/llama.cpp)


Prerequisites
-------------
*   *Visual Studio Community* installed with *Desktop C++ Environment* selected during installation
*   *[Chocolatey](https://chocolatey.org/)* (a package manager for Windows) installed
*   *[CMake](https://cmake.org/download/)* installed
*   Python 3 installed
*   LLaMA models downloaded  ([dalai](https://github.com/cocktailpeanut/dalai) can help)


Steps
-------------
## install make
Install Make Open PowerShell as an administrator and run the following command:

```powershell
choco install make
```

##  python
if python is not installed, you can install python via choco
```powershell
choco install python
```

## clone llama.cpp
Clone repository using Git or download the repository as a ZIP file and extract it to a directory on your machine.

[llama.cpp](https://github.com/ggerganov/llama.cpp)

## build llama.cpp
Use *Visual Studio* to open llama.cpp directory.

Select "View" and then "Terminal" to open a command prompt within Visual Studio. Type the following commands:

```powershell
cmake .
make
```

On the right hand side panel:

    right click file `quantize.vcxproj` -> select build
    this output .\Debug\quantize.exe


    right click `ALL_BUILD.vcxproj` -> select build
    this output .\Debug\llama.exe

## create a python virtual environment
back to the powershell termimal, cd to lldma.cpp directory, suppose `LLaMA model`s have been download to models directory

```powershell
python -m venv
.\venv\Scripts\pip.exe install torch torchvision torchaudio sentencepiece numpy

.\venv\Scripts\python.exe convert-pth-to-ggml.py models/7B/ 1

.\Debug\quantize.exe ./models/7B/ggml-model-f16.bin ./models/7B/ggml-model-q4_0.bin 2

.\Debug\llama.exe -m ./models/7B/ggml-model-q4_0.bin -t 8 -n 128
```
