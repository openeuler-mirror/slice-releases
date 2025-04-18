# slice-releases

#### 介绍
这里保存着openEuler官方软件的slice定义文件（Slice Definition File， SDF）源码, 用于[splitter](https://gitee.com/openeuler/splitter)生成构建distroless容器镜像的slices。

#### Slice Releases
每个openEuler版本的slice release由不同的分支承载，且分支以对应的openEuler版本命名。当前官方支持的slice release如下：
- [`openEuler-24.03-LTS`](https://gitee.com/openeuler/slice-releases/tree/openEuler-24.03-LTS/)

#### SDF说明
SDF定义了openEuler软件包切分成不同slice的规则，软件包`A`的SDF文件格式如下：
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

SDF的文件名为`{package}.yaml`, `{package}`是软件包名，内容如下：
- `package`: 软件包，与文件名对应
- `deps`: 依赖的slice
- `slices`: 所有的slice
- `contents`: 每个slice包含的文件，其中：
    - `common`: slice包含的基础文件范围
    - `extra`: slice依赖的从软件包外部引入或不同架构定制的内容
- `copyright`: 软件lisence


#### 如何使用
slice releases与[splitter](https://gitee.com/openeuler/splitter)一起使用。在使用splitter切分软件包生成slice时，用户必须指定通过`--release`指定slice release>

#### 参与贡献
欢迎广大开发者参与openEuler distroless镜像生态建设！

1. 请提issue描述对更多distroless镜像的需求，并与社区讨论、开发相关SDF
2. 对distroless容器构建有更优的实现，请提PR至[splitter](https://gitee.com/openeuler/splitter)仓库