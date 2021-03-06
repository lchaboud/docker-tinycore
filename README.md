Tiny Core Linux Docker Image
============================

This provides a very small CLI system image based on Tiny Core Linux developed
at [The Core Project](http://tinycorelinux.net). It contains following Core
6.0 x86/x86\_64 packages

- rootfs.gz (or rootfs64.gz): contains base system binaries and a file system
  layout
- squashfs-tools.tcz: contains a squashfs builder and expander

These original packages are found under http://tinycorelinux.net/6.x/ and
Dockerfile of these images are found at

- 6.0-x86:
  [x86/Dockerfile](https://github.com/tatsushid/docker-tinycore/blob/master/x86/Dockerfile)
- 6.0-x86\_64:
  [x86\_64/Dockerfile](https://github.com/tatsushid/docker-tinycore/blob/master/x86_64/Dockerfile)

## Installation

The easiest way to install the image is pulling it from
[Docker Hub repositories](https://registry.hub.docker.com/) like following

```bash
docker pull tatsushid/tinycore:6.0-x86
```

or

```bash
docker pull tatsushid/tinycore:6.0-x86_64
```

## Usage

Just run

```bash
docker run -it tatsushid/tinycore:6.0-x86
```

or

```bash
docker run -it tatsushid/tinycore:6.0-x86_64
```

To install tcz packages into the container and use them, please run `tce-load`
command in it like following

```bash
tce-load -wic bash.tcz
```

or run the container with privilege mode like following

```bash
docker run -it --privileged tatsushid/tinycore:6.0-x86
```

Once it starts with privilege mode, you can run the package manager like

```bash
tce-ab
```

## Building an image based on this image

Now Docker doesn't support privilege mode at image building but this image
includes patched `tce-load` which works without privilege mode by using
`unsquashfs` internally instead of mounting squashfs on a loop back device so
to install packages, please use `tce-load` with `-c` option
