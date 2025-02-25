:warning: Development of this fork has been moved to [rsudp-leq](https://github.com/rodonile/rsudp-leq). :warning:

# About this fork:

- [Rsudp](https://github.com/raspishake/rsudp) extended to plot intensity and equivalent continuous sound level (Leq) 
- Added new alarm modules (c_alarm_leq.py and c_alarm_leq_iir.py) which trigger alarms based on short-term vs long-term Leq calculation
- Coded and tested only for RS1D / 1 channel geophone
- Differences with upstream: [GithubCompare](https://github.com/raspishake/rsudp/compare/master...rodonile:master)
- **For production deployment:** minimal version which works also on Windows OS (with fewer modules and dependencies) available on the ~~*windows* branch~~ [rsudp-leq](https://github.com/rodonile/rsudp-leq) repo.

## Use-cases:

- Main goal: small disturbance detection, i.e. trigger alarm on trains nearby, construction work, etc. that might disturb measurements in acoustically controlled environments 

## The enhanced live-plotting module:
![GUI](docs/_images/rsudp_gui_rodonile.png)

(dB reference value: 1 $\mu m/s$)


## Installation instruction (Linux)
Clone this repo, then run:

    cd rsudp
    bash unix-install-rsudp.sh

The script should take care of the installation automatically. In case you encounter any errors, try to manually [install miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html) before re-running the script. 


## How to start the program

    conda activate rsudp
    rs-client

The program assumes the configuration file is located at *~/.config/rsudp/rsudp_settings.json*, which should be the case if rsudp was installed with the setup script. Alternatively you can run the program specifying the location of the configuration file:

    rs-client -d /path/to/config/file

## Configuration parameters

An explanation of the most important parameters in the *rsudp_settings.json* file is available in the [configuration_file](rsudp/configuration_file) folder.  


# rsudp main README:
### Continuous sudden motion and visual monitoring of Raspberry Shake data
*Written by Ian Nesbitt (@iannesbitt), Richard Boaz, and Justin Long (@crockpotveggies)*

[![PyPI](https://img.shields.io/pypi/v/rsudp)](https://pypi.org/project/rsudp/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/rsudp)](https://pypi.org/project/rsudp/)
[![GitHub](https://img.shields.io/github/license/raspishake/rsudp)](https://github.com/raspishake/rsudp/blob/master/LICENSE)
[![Documentation](https://img.shields.io/badge/docs-passed-brightgreen)](https://raspishake.github.io/rsudp/)
[![Build Status](https://scrutinizer-ci.com/g/raspishake/rsudp/badges/build.png?b=master)](https://scrutinizer-ci.com/g/raspishake/rsudp/build-status/master)
[![Code Coverage](https://scrutinizer-ci.com/g/raspishake/rsudp/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/raspishake/rsudp/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/raspishake/rsudp/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/raspishake/rsudp/?branch=master)
[![DOI](https://joss.theoj.org/papers/10.21105/joss.02565/status.svg)](https://doi.org/10.21105/joss.02565)

`rsudp` is a tool for receiving and interacting with data casts from [Raspberry Shake](https://raspberryshake.org) personal seismographs and Raspberry Boom pressure transducer instruments.

`rsudp` has [full documentation here](https://raspishake.github.io/rsudp/). We also have [tutorial instructions](https://raspishake.github.io/rsudp/index.html#tutorial) to install, set up, and run `rsudp` there. Additionally, our documentation features [YouTube walkthroughs](https://raspishake.github.io/rsudp/youtube.html), [notes for contributors](https://raspishake.github.io/rsudp/contributing.html), a brief [Developer's guide](https://raspishake.github.io/rsudp/theory.html), and [module documentation](https://raspishake.github.io/rsudp/#code-documentation).

We now have [a paper](https://doi.org/10.21105/joss.02565) published in The Journal of Open Source Software! You can reference `rsudp` using the following citation:

> Nesbitt et al., (2021). rsudp: A Python package for real-time seismic monitoring with Raspberry Shake instruments. Journal of Open Source Software, 6(68), 2565, https://doi.org/10.21105/joss.02565


`rsudp` contains ten main features:
1. **Alert** - an earthquake/sudden motion alert trigger, complete with a bandpass filter and stream deconvolution capabilities
2. **AlertSound** - a thread that plays a MP3 audio file in the event of the alert module signalling an alarm state
3. **Plot** - a live-plotting routine to display data as it arrives on the port, with an option to save plots some time after an alarm
4. **Tweeter** - a thread that broadcasts a Twitter message when the alert module is triggered, and optionally can tweet saved plots from the plot module
5. **Telegrammer** - a thread similar to the Tweeter module that sends a [Telegram](https://telegram.org) message when an alarm is triggered, which can also broadcast saved images
6. **Writer** - a simple miniSEED writer
7. **Forward** - forward a data cast to one or several IP/port destinations
8. **RSAM** - computes RSAM (Real-time Seismic AMplitude) and either prints or forwards it to an IP/port destination
9. **Custom** - run custom code when an `ALARM` message is received
10. **Print** - a debugging tool to output raw data to the command line

`rsudp` is written in Python but requires no coding knowledge to run. Simply follow the [instructions to install the software](https://raspishake.github.io/rsudp/installing.html), go to your Shake's web front end, [configure a UDP datacast](https://manual.raspberryshake.org/udp.html#configuring-a-data-stream-the-easy-way) to your computer's local IP address, [start the software](https://raspishake.github.io/rsudp/running.html) from the command line, and watch the data roll in.