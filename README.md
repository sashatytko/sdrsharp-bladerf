# sdrsharp-bladerf

bladeRF driver for SDR#

![fm_band](https://github.com/sashatytko/sdrsharp-bladerf/assets/27360903/022c9275-1da0-479f-b9cb-762df6334ef7)


Original repos:

https://github.com/jmichelp/sdrsharp-bladerf

https://github.com/Nuand/sdrsharp-bladerf

# Changes in this fork

1. Fixed frequency ranges for BladeRF2 (BladeRF xA4, BladeRF xA5, BladeRF xA9)
2. Changed gain control mode to manual
3. Fixed bug that crash SDR# when stop receiving
4. Made generation of available sample rates according to BladeRF board version

# Notes

The latest SDRSharp version compatiable with BladeRF is 1.0.0.1732. I am unable to make work pure SDRSharp v1.0.0.1732 with BladeRF, that`s why you should download specific (patched) SDRSharp v1.0.0.1732 provided in release section. 

In release libbladeRF v2.0.2 is in use, newer versions might break compatibility with BladeRF1 (BladeRF x40, Bladerf x115).

Code refactor was not done because driver might be compatible with BladeRF1 (BladeRF x40, Bladerf x115) and I do not have hardware to test changes.

All source code, precompiled .dll and SDRSharp v1.0.0.1732 available in [release page](https://github.com/sashatytko/sdrsharp-bladerf/releases/tag/release).


## Installation

### Windows

#### Precompiled binaries

1. Download the [precompiled SDR# plugin binaries (dll)](https://github.com/sashatytko/sdrsharp-bladerf/releases/tag/release)
2. Unzip to SDR# directory
3. Launch SDR#

#### Compiling from source

1. Copy the Release\SDRSharp.BladeRF.dll into SDR# installation directory
2. If required, copy all DLL files from LibBladeRF subdirectory to SDR# installation directory
3. Add the following line in the frontendPlugins sections of FrontEnds.xml file:

	&lt;add key="BladeRF" value="SDRSharp.BladeRF.BladeRFIO,SDRSharp.BladeRF" /&gt;


4. Launch SDR# and cross fingers :)

**Be aware that any update of SDR# will require you to follow again steps 2 to 4!**

### Linux

To use SDR# on Linux, you need to first install a version of Mono that supports .Net framework 4.6.

At the moment, the setup has been tested using Mono 4.4.0.40 and is working.


1. Copy the Release/SDRSharp.BladeRF.dll into SDR# installation directory
2. Symlink required libraries in the SDR# installation directory:

	```bash
	$ ln -s /usr/lib/libportaudio.so.2 libportaudio.so
	$ ln -s /usr/local/lib/libbladeRF.so .
	```

3. Add the following line in the frontendPlugins sections of FrontEnds.xml file:

	&lt;add key="BladeRF" value="SDRSharp.BladeRF.BladeRFIO,SDRSharp.BladeRF" /&gt;


4. Launch SDR# and cross fingers :)

**Be aware that any update of SDR# will require you to follow again steps 2 to 4!**

## Troubleshooting

If your samples look "weird" under SDR#, be sure to use a compatible libusb-1.0.dll.
Specially when frequently upgrading SDR#, it will re-install the RTL-SDR driver which embedds a pretty old version of this DLL (v.1.0.14).
The version provided under LibBladeRF directory of this repository (currently v1.0.19) is known to work correcly with both RTL-SDR dongles and BladeRF. So it is safe (and recommended) to replace it.

If this does not solve your issue, feel free to report a bug here. I will try to fix it as soon as possible.
Same goes for new features.


## Compilation

If you need/want to compile this DLL, you need to copy the following two DLL files
from SDR# installation directory to Release and/or Debug directories:

1. SDRSharp.Radio.dll
2. SDRSharp.Common.dll

Compiling under Linux is also possible using Mono 4.4.0.40+ (even if a warning is issued to tell that building with framework 4.6 is
not supported.

Be aware that Mono xbuild uses different pathes for compilation so you will need to copy the 2 aforementioned DLL files in the
building directory expected by Mono xbuild for the compilation to succeed.


## Bugs? Ideas?

Please report them using the bugtracker on the Github project!
