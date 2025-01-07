# PICO-Template Setup for Raspberry Pi Microcontrollers

This project is all about getting started with Raspberry Pi microcontrollers. Below you’ll find the steps to set up the **PICO-Template**, including how to clone the repository, configure OpenOCD for debugging, and tweak the project for your specific platform.

## 1. Clone This Repo Recursively

First things first, grab the repo (including submodules) with:

```bash
git clone --recursive https://github.com/nickfox-taterli/PICO-Template
```

If you’ve already cloned it without `--recursive`, you can still fetch submodules by running:

```bash
git submodule update --init --recursive
```

## 2. Download the Official OpenOCD

Next, you’ll need the official OpenOCD from Raspberry Pi. The source is here:

- **GitHub Repo**: [https://github.com/raspberrypi/pico-sdk-tools/releases](https://github.com/raspberrypi/pico-sdk-tools/releases)

Pick the release package that suits your architecture (for example, `openocd-0.12.0+dev-x64-win.exe` if you’re using 64-bit Windows). 

After installing or extracting, you need to arrange the directory structure so it looks like this:

```
OpenOCD
├─openocd
│  ├─bin
│  └─scripts
│      ├─board
│      │  └─gti
│      ├─chip
│      │  ├─atmel
│      │  │  └─at91
│      │  ├─st
│      │  │  ├─spear
│      │  │  └─stm32
│      │  └─ti
│      │      └─lm3s
│      ├─cpld
│      ├─cpu
│      │  ├─arc
│      │  └─arm
│      ├─fpga
│      ├─interface
│      │  ├─ft232r
│      │  └─ftdi
│      ├─target
│      │  ├─geehy
│      │  ├─infineon
│      │  └─marvell
│      ├─test
│      └─tools
```

Essentially, make sure the contents are placed in the right folders under `openocd/bin` and `openocd/scripts`.

## 3. Configure CLion to Use This OpenOCD

Open the project in CLion and go to **File → Settings → Build, Execution, Deployment → Embedded Development → OpenOCD**.  
Point this setting to the newly extracted **OpenOCD** path you created above.

## 4. Adjust the CMakeLists.txt if Needed

In the `CMakeLists.txt`, there’s a line:

```cmake
set(PICO_PLATFORM "rp2350" CACHE STRING "Target platform for the Pico project")
```

- If you’re on a different platform, go ahead and modify `"rp2350"` to something else that matches your hardware.

## 5. Non-Windows Platforms

If you’re not on Windows, you’ll also want to replace the files in the `picotool` directory inside the project with their Linux or Mac equivalents. The default files might be configured for Windows, so you’ll need to adjust those accordingly.

## 6. Double-Check `openocd.cfg`

Inside the `picotool` folder, there’s an `openocd.cfg` set up for **picoprobe**. If you’re using a different probe, you’ll need to tweak this file to match your setup. For compilers, make sure you have a suitable toolchain installed or use one of the prebuilt toolchains.

## 7. Alternatively, Grab a Complete Project

If you want a quick start (and don’t want to fiddle with CLion settings), you can also download a complete project with the `.idea` directory from the **releases** page. That should give you a working reference out of the box.

---

**Happy coding and debugging!** If you run into any issues, feel free to open an issue in the repo or check the discussions for more info.