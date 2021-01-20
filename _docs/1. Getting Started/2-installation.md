---
title: "Installation"
permalink: /installation/
excerpt: "Installation instructions for VSGAN."
last_modified_at: 2021-01-20T23:26:00-00:00
toc: true
---

## Hardware Requirements

**GPU:** NVIDIA GPU that has support for CUDA 9.2+. A CUDA Compute Capability score of 6 or higher is recommended, and a score <= 2 will be incredibly slow, if it works at all.  
**CPU:** There's no specific requirement for the CPU, just try and use a CPU that won't bottle-neck your GPU. The CPU will be used, but not much.

**No Supported GPU?** If you don't mind waiting minutes or even hours per frame, then you can use your CPU instead of the GPU. Just note that it's not our responsibility if over-use of your CPU, lower it's life span, or even get it killed. Expect constantly high CPU Usage and Temperatures causing even your mouse to lag.

## Dependencies

These are software you need installed which cannot be done automatically during installation. Install in the listed order. The latest version of all dependencies are recommended.

1. [**Python 3.5+**][Python] & [**pip**][pip]
2. [**VapourSynth**][VapourSynth]
3. [**PyTorch 1.6.0+**][PyTorch]. Ensure you install PyTorch with CUDA support if you plan to use your GPU.
4. [**NVIDIA CUDA 9.2+**][CUDA]. Ensure the version is supported by the version of PyTorch that you chose.

**Tip for Python & pip:** Ensure Python is added to PATH for an optimal Python environment and swift installation;
When installing, Tick `Add Python X.X to PATH` in `Customize Installation` mode.
Pip may come pre-installed, run `pip -V` and if it tells you `pip x.x.x from xyz (python x.x)` then it's installed.
{: .notice--info}

**Tip for VapourSynth:** When installing VapourSynth, ensure you follow all the instructions on their [official website][VapourSynth] for your OS.
There are important instructions specific to each OS.
The Pip/PyPI package `VapourSynth` is *not* the VapourSynth dependency that you need to install.
{: .notice--info}

## Installing VSGAN

```bash
pip install vsgan
```

**Tip:** Do not run pip under Administrator/Sudo permissions. See [Pip as Admin]({{ '/pip-as-admin/' | relative_url }}).
{: .notice--warning}

You may also install from source; Check out [Building]({{ '/building' | relative_url }}).
{: .notice--info}

Once installed, make sure you give yourself a refresher on [Updating]({{ '/updating' | relative_url }}).
{: .notice--success}

  [Python]: https://python.org
  [pip]: https://pip.pypa.io/en/stable/installing
  [VapourSynth]: https://vapoursynth.com
  [PyTorch]: https://pytorch.org/get-started/locally
  [CUDA]: https://developer.nvidia.com/cuda-downloads
