# asitop

![PyPI - Downloads](https://img.shields.io/pypi/dm/asitop)

Performance monitoring CLI tool for Apple Silicon

![](images/asitop.png?v=2)

```shell
# Install this custom fork using uv (Recommended)
uv tool install git+[https://github.com/DanVicenteIhanus/asitop.git](https://github.com/YOUR_USERNAME/asitop.git)

# Or install using pip
pip install git+[https://github.com/YOUR_USERNAME/asitop.git](https://github.com/YOUR_USERNAME/asitop.git)
```

## What is `asitop`

A Python-based `nvtop`-inspired command line tool for Apple Silicon (M-series) Macs.

* Utilization info:
  * CPU (E-cluster and P-cluster), GPU
  * Frequency and utilization
  * ANE utilization (measured by power)
* Memory info:
  * RAM and swap, size and usage
  * (Apple removed memory bandwidth from `powermetrics`)
* Power info:
  * CPU power, GPU power (Apple removed package power from `powermetrics`)
  * Chart for CPU/GPU power
  * Peak power, rolling average display
* **NEW:** Minimal GPU-only mode (`--gpu_only`) for a distraction-free GPU gauge and power chart.

`asitop` uses the built-in [`powermetrics`](https://www.unix.com/man-page/osx/1/powermetrics/) utility on macOS, which allows access to a variety of hardware performance counters. Note that it requires `sudo` to run due to `powermetrics` needing root access to run. `asitop` is lightweight and has minimal performance impact.

**`asitop` only works on Apple Silicon Macs!**

## Installation and Usage

`asitop` is a Python-based command line tool. This fork is best installed globally using `uv`. After installation, you can use it via the Terminal.

```shell
# to enter password before start
# this mode is recommended!
sudo asitop

# start in minimal GPU-only mode
sudo asitop --gpu_only

# it will prompt password on start
asitop

# advanced options
asitop [-h] [--interval INTERVAL] [--color COLOR] [--avg AVG] [--gpu_only]
optional arguments:
  -h, --help           show this help message and exit
  --interval INTERVAL  Display interval and sampling interval for powermetrics (seconds)
  --color COLOR        Choose display color (0~8)
  --avg AVG            Interval for averaged values (seconds)
  --gpu_only           Show only GPU usage and power
```

## How it works

`powermetrics` is used to measure the following:

* CPU/GPU utilization via active residency
* CPU/GPU frequency
* Package/CPU/GPU/ANE energy consumption
* CPU/GPU/Media Total memory bandwidth via the DCS (DRAM Command Scheduler)

[`psutil`](https://github.com/giampaolo/psutil) is used to measure the following:

* memory and swap usage

[`sysctl`](https://developer.apple.com/library/archive/documentation/System/Conceptual/ManPages_iPhoneOS/man3/sysctl.3.html) is used to measure the following:

* CPU name
* CPU core counts

[`system_profiler`](https://ss64.com/osx/system_profiler.html) is used to measure the following:

* GPU core count

Some information is guesstimate and hardcoded as there doesn't seem to be an official source for it on the system:

* CPU/GPU TDP
* CPU/GPU maximum memory bandwidth
* ANE max power
* Media engine max bandwidth

## Why the fork

Because I use Asitop from time to time to monitor hardware usage, but typically am only interested in the GPU. So wanted a minimal GUI, to just monitor the GPU.

## Disclaimers

I did this randomly don't blame me if it fried your new MacBook or something.
