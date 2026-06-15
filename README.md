<div align="center">

# BleachBit Packaging

BleachBit system cleaner packaging resources for Windows and Linux builds, with Debian and Ubuntu package workflows using Open Build Service.

</div>

## 🧹 Overview

BleachBit is a system cleaner for Windows and Linux. This repository contains resources used for building BleachBit packages with the openSUSE Open Build Service (OBS).

The documented workflow focuses on Debian and Ubuntu package builds managed through the `osc` command-line tool. OBS is used to check out package definitions, run local builds, submit changes, branch packages for testing, and inspect build results.

## 📦 Open Build Service

Open Build Service documentation for Debian builds:

https://en.opensuse.org/openSUSE:Build_Service_Debian_builds

OBS project page with build status and packages:

https://build.opensuse.org/package/show/home:andrew_z/bleachbit

## 🛠️ Debian and Ubuntu Package Build Workflow

Install the [`osc`](https://github.com/openSUSE/osc) tool before working with OBS packages.

An account on https://build.opensuse.org/ is required for OBS operations. See this discussion for background:

https://github.com/openSUSE/osc/issues/812

### Check out package files from OBS

```bash
osc checkout home:andrew_z bleachbit -o /tmp/obsfiles
diff -u3 /tmp/obsfiles .
```

Checkout syntax:

```bash
osc co <project> <package> --outdir <path>
```

### Run a local build

From an `osc` checkout, run:

```bash
osc build xUbuntu_20.10
```

`xUbuntu_20.10` is an example repository name configured in OBS.

### Branch the OBS package for test builds

```bash
osc branch home:andrew_z bleachbit
```

After branching, OBS prints the checkout command for the branched package, for example:

```bash
osc co home:abitrolly:branches:home:andrew_z/bleachbit
```

### Inspect build status and logs

Use `osc results` to view build status:

```bash
osc results
```

Example output:

```text
xUbuntu_20.10        x86_64     failed
xUbuntu_20.04        x86_64     succeeded*
xUbuntu_18.04        x86_64     succeeded*
```

Use `osc buildlog` to inspect build output for a repository:

```bash
osc buildlog xUbuntu_20.10
```

More `osc` commands are available in the OBS cheat sheet:

https://en.opensuse.org/images/d/df/Obs-cheat-sheet.pdf

## 🔎 Notes

- The workflow described here is centered on OBS package maintenance.
- `osc` is used to check out, build, branch, submit, and inspect OBS packages.
- Build results depend on the configured OBS repositories and package state.
