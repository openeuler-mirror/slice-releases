English | [中文](README.md)

# slice-releases

#### Introduction
This repository contains the Slice Definition File (SDF) source code for openEuler's official software packages. These SDFs are processed by [splitter](https://gitee.com/openeuler/splitter) to produce slices for constructing distroless container images.

#### Slice Releases
Slice releases for different openEuler versions are hosted in version-specific branches (named by openEuler releases). Below is the list of currently supported official slice releases:
- [`openEuler-24.03-LTS`](https://gitee.com/openeuler/slice-releases/tree/openEuler-24.03-LTS/)

#### Slice Definition Files
SDFs define how openEuler packages are splitted into discrete slices. Below is the SDF format for package `A`:
```
# A.yaml
package: A

deps:
  - A_copyright

slices:
  slice1:
    deps:
      - B_slice1
  slice2:
    deps:
      - C_slice2
    contents:
      common:
        - /path/to/content1
        - /path/to/content2
        - /path/to/content3
      extra:
        linux-aarch64:
          - /path/to/content4
        copy:
          - /path/to/content5: /outside/path/to/content5
        ...
  copyright:
    contents:
      common:
        - /path/to/content6
```

The SDF adopts a `{package}.yaml` naming convention (where `{package}` is the software name) and contains these fields:
- `package`: Name (must match filename)
- `deps`: slice dependencies
- `slices`: list of all slices
- `contents`: Per-slice file specifications：
    - `common`: public files
    - `extra`: external/architecture-dependent components
- `copyright`: lisence


#### Usage
Slice releases work with [splitter](https://gitee.com/openeuler/splitter). To generate slices by splitting packages, the `--release` argument is required to select the target slice release.

#### Contribution
Welcome to contribute to openEuler’s distroless ecosystem!

1. **Request new images:** File issues to discuss SDF development.
2. **Enhance the toolchain:** Submit PRs to [splitter](https://gitee.com/openeuler/splitter) with improvements.