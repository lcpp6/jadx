# 该项目对于安卓开发人员有一些值得参考的意义：
### 1、如果你要在安卓上使用，可以参考这个示例：[jadx-lib-android-example](https://github.com/jadx-decompiler/jadx-lib-android-example)
jadx这个项目主要是对apk（即dex）反编译成为 java。\
上面这个示例是反编译多个dex（也就是apk里面的全部dex ）\
但是也提供了其他输入插件，比如dex、smali、等，请参考以下命令。

但是我建议在安卓上每次单独反编译一个Smali文件，而不是dex。

一个smali这样速度快很多

### 2、如果你要在安卓上实现插件系统，也可以参考其中的插件实现方式。


### 3、命令中文翻译参考
```
jadx[-gui] [命令] [选项] <输入文件> (.apk, .dex, .jar, .class, .smali, .zip, .aar, .arsc, .aab, .xapk, .jadx.kts)
命令（使用 '<命令> --help' 查看命令选项）：
  plugins	  - 管理jadx插件

选项：
  -d, --output-dir                      - 输出目录
  -ds, --output-dir-src                 - 源代码的输出目录
  -dr, --output-dir-res                 - 资源的输出目录
  -r, --no-res                          - 不解码资源
  -s, --no-src                          - 不反编译源代码
  --single-class                        - 反编译单个类，完整名称，原始或别名
  --single-class-output                 - 如果反编译单个类，则为写入文件或目录
  --output-format                       - 可以是 'java' 或 'json'，默认：java
  -e, --export-gradle                   - 保存为Android Gradle项目
  -j, --threads-count                   - 处理线程数，默认：4
  -m, --decompilation-mode              - 代码输出模式：
                                           'auto' - 尝试最佳选项（默认）
                                           'restructure' - 恢复代码结构（普通Java代码）
                                           'simple' - 简化指令（线性，带goto）
                                           'fallback' - 原始指令不修改
  --show-bad-code                       - 显示不一致的代码（错误反编译）
  --no-xml-pretty-print                 - 不美化XML
  --no-imports                          - 禁用导入使用，始终写入完整包名
  --no-debug-info                       - 禁用调试信息解析和处理
  --add-debug-lines                     - 如果可用，添加带有调试行号的注释
  --no-inline-anonymous                 - 禁用匿名类内联
  --no-inline-methods                   - 禁用方法内联
  --no-move-inner-classes               - 禁用将内部类移动到父类
  --no-inline-kotlin-lambda             - 禁用Kotlin lambdas内联
  --no-finally                          - 不提取finally块
  --no-restore-switch-over-string       - 不恢复switch over string
  --no-replace-consts                   - 不用匹配的常量字段替换常量值
  --escape-unicode                      - 在字符串中转义非拉丁字符（使用 \u）
  --respect-bytecode-access-modifiers   - 不改变原始访问修饰符
  --mappings-path                       - 反混淆映射文件或目录。允许的格式：Tiny和Tiny v2（两者都是'.tiny'），Enigma（'.mapping'）或Enigma目录
  --mappings-mode                       - 设置处理反混淆映射文件的模式：
                                           'read' - 仅读取，用户可以随时手动保存（默认）
                                           'read-and-autosave-every-change' - 每次更改后读取并自动保存
                                           'read-and-autosave-before-closing' - 退出应用程序或关闭项目前读取并自动保存
                                           'ignore' - 不读取或保存（可以用来跳过项目文件中引用的映射文件加载）
  --deobf                               - 激活反混淆
  --deobf-min                           - 名称的最小长度，如果更短则重命名，默认：3
  --deobf-max                           - 名称的最大长度，如果更长则重命名，默认：64
  --deobf-whitelist                     - 排除反混淆的类（完整名称）和包（以'.*'结尾）的空格分隔列表，默认：android.support.v4.* android.support.v7.* android.support.v4.os.* android.support.annotation.Px androidx.core.os.* androidx.annotation.Px
  --deobf-cfg-file                      - 用于JADX自动生成名称的反混淆映射文件（JOBF文件格式），默认：与输入文件相同目录和名称，扩展名为'.jobf'
  --deobf-cfg-file-mode                 - 设置处理JADX自动生成名称的反混淆映射文件的模式：
                                           'read' - 如果找到则读取，不保存（默认）
                                           'read-or-save' - 如果找到则读取，否则保存（不覆盖）
                                           'overwrite' - 不读取，始终保存
                                           'ignore' - 不读取也不保存
  --deobf-res-name-source               - 更好的资源名称来源：
                                           'auto' - 自动选择最佳名称（默认）
                                           'resources' - 使用资源名称
                                           'code' - 使用R类字段名称
  --use-source-name-as-class-name-alias - 将源名称用作类名别名：
                                           'always' - 如果可用，始终使用源名称
                                           'if-better' - 如果似乎比当前名称更好，则使用源名称
                                           'never' - 即使可用，也从不使用源名称
  --use-kotlin-methods-for-var-names    - 使用Kotlin内置方法重命名变量，值：禁用，应用，应用并隐藏，默认：应用
  --rename-flags                        - 修复选项（逗号分隔列表）：
                                           'case' - 修复大小写敏感性问题（根据--fs-case-sensitive选项），
                                           'valid' - 将Java标识符重命名为有效名称，
                                           'printable' - 从标识符中删除不可打印字符，
                                           或单个 'none' - 禁用所有重命名
                                           或单个 'all' - 启用所有（默认）
  --integer-format                      - 如何显示整数：
                                           'auto' - 自动选择（默认）
                                           'decimal' - 使用十进制
                                           'hexadecimal' - 使用十六进制
  --fs-case-sensitive                   - 将文件系统视为大小写敏感，默认为false
  --cfg                                 - 将方法控制流图保存到dot文件
  --raw-cfg                             - 保存方法控制流图（使用原始指令）
  -f, --fallback                        - 将 '--decompilation-mode' 设置为 'fallback'（已弃用）
  --use-dx                              - 使用dx/d8将Java字节码转换
  --comments-level                      - 设置代码注释级别，值：错误，警告，信息，调试，仅用户，默认：信息
  --log-level                           - 设置日志级别，值：安静，进度，错误，警告，信息，调试，默认：进度
  -v, --verbose                         - 详细输出（将 --log-level 设置为 DEBUG）
  -q, --quiet                           - 关闭输出（将 --log-level 设置为 QUIET）
  --version                             - 打印jadx版本
  -h, --help                            - 打印此帮助

插件选项（-P<名称>=<值>）：
  dex-input: 加载.dex和.apk文件
    - dex-input.verify-checksum         - 在加载前验证dex文件的校验和，值：[是，否]，默认：是
  java-convert: 将.class, .jar和.aar文件转换为dex
    - java-convert.mode                 - 转换模式，值：[dx, d8, 两者]，默认：两者
    - java-convert.d8-desugar           - 在d8中使用desugar，值：[是，否]，默认：否
  kotlin-metadata: 使用kotlin.Metadata注解进行代码生成
    - kotlin-metadata.class-alias       - 重命名类别名，值：[是，否]，默认：是
    - kotlin-metadata.method-args       - 重命名函数参数，值：[是，否]，默认：是
    - kotlin-metadata.fields            - 重命名字段，值：[是，否]，默认：是
    - kotlin-metadata.companion         - 重命名伴随对象，值：[是，否]，默认：是
    - kotlin-metadata.data-class        - 添加数据类修饰符，值：[是，否]，默认：是
    - kotlin-metadata.to-string         - 使用toString重命名字段，值：[是，否]，默认：是
    - kotlin-metadata.getters           - 将简单getter重命名为字段名称，值：[是，否]，默认：是
  rename-mappings: 各种映射支持
    - rename-mappings.format            - 映射格式，值：[AUTO, TINY_FILE, TINY_2_FILE, ENIGMA_FILE, ENIGMA_DIR, SRG_FILE, XSRG_FILE, JAM_FILE, CSRG_FILE, TSRG_FILE, TSRG_2_FILE, PROGUARD_FILE, RECAF_SIMPLE_FILE, JOBF_FILE]，默认：AUTO
    - rename-mappings.invert            - 加载时反转映射，值：[是，否]，默认：否
  smali-input: 加载.smali文件
    - smali-input.api-level             - Android API级别，默认：27

环境变量：
  JADX_DISABLE_XML_SECURITY - 设置为 'true' 以禁用所有XML文件的安全检查
  JADX_DISABLE_ZIP_SECURITY - 设置为 'true' 以禁用所有zip文件的安全检查
  JADX_ZIP_MAX_ENTRIES_COUNT - zip文件中允许的最大条目数（默认：100,000）
  JADX_CONFIG_DIR - 自定义

```

----

<img src="https://raw.githubusercontent.com/skylot/jadx/master/jadx-gui/src/main/resources/logos/jadx-logo.png" width="64" align="left" />

## JADX

![Build status](https://img.shields.io/github/actions/workflow/status/skylot/jadx/build-artifacts.yml)
![GitHub contributors](https://img.shields.io/github/contributors/skylot/jadx)
![GitHub all releases](https://img.shields.io/github/downloads/skylot/jadx/total)
![GitHub release (latest by SemVer)](https://img.shields.io/github/downloads/skylot/jadx/latest/total)
![Latest release](https://img.shields.io/github/release/skylot/jadx.svg)
[![Maven Central](https://img.shields.io/maven-central/v/io.github.skylot/jadx-core)](https://search.maven.org/search?q=g:io.github.skylot%20AND%20jadx)
![Java 11+](https://img.shields.io/badge/Java-11%2B-blue)
[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

**jadx** - Dex to Java decompiler

Command line and GUI tools for producing Java source code from Android Dex and Apk files

> [!WARNING]
> Please note that in most cases **jadx** can't decompile all 100% of the code, so errors will occur.<br />
> Check [Troubleshooting guide](https://github.com/skylot/jadx/wiki/Troubleshooting-Q&A#decompilation-issues) for workarounds.

**Main features:**
- decompile Dalvik bytecode to Java code from APK, dex, aar, aab and zip files
- decode `AndroidManifest.xml` and other resources from `resources.arsc`
- deobfuscator included

**jadx-gui features:**
- view decompiled code with highlighted syntax
- jump to declaration
- find usage
- full text search
- smali debugger, check [wiki page](https://github.com/skylot/jadx/wiki/Smali-debugger) for setup and usage

Jadx-gui key bindings can be found [here](https://github.com/skylot/jadx/wiki/JADX-GUI-Key-bindings)

See these features in action here: [jadx-gui features overview](https://github.com/skylot/jadx/wiki/jadx-gui-features-overview)

<img src="https://user-images.githubusercontent.com/118523/142730720-839f017e-38db-423e-b53f-39f5f0a0316f.png" width="700"/>

### Download
- release
  from [github: ![Latest release](https://img.shields.io/github/release/skylot/jadx.svg)](https://github.com/skylot/jadx/releases/latest)
- latest [unstable build ![GitHub commits since tagged version (branch)](https://img.shields.io/github/commits-since/skylot/jadx/latest/master)](https://nightly.link/skylot/jadx/workflows/build-artifacts/master)

After download unpack zip file go to `bin` directory and run:
- `jadx` - command line version
- `jadx-gui` - UI version

On Windows run `.bat` files with double-click\
**Note:** ensure you have installed Java 11 or later 64-bit version.
For Windows, you can download it from [oracle.com](https://www.oracle.com/java/technologies/downloads/#jdk17-windows) (select x64 Installer).

### Install
- Arch Linux
  [![Arch Linux package](https://img.shields.io/archlinux/v/extra/any/jadx)](https://archlinux.org/packages/extra/any/jadx/)
  [![AUR Version](https://img.shields.io/aur/version/jadx-git)](https://aur.archlinux.org/packages/jadx-git)
  ```bash
  sudo pacman -S jadx
  ```
- macOS
  [![homebrew version](https://img.shields.io/homebrew/v/jadx)](https://formulae.brew.sh/formula/jadx)
  ```bash
  brew install jadx
  ```
- Flathub
  [![Flathub Version](https://img.shields.io/flathub/v/com.github.skylot.jadx)](https://flathub.org/apps/com.github.skylot.jadx)
  ```bash
  flatpak install flathub com.github.skylot.jadx
  ```

### Use jadx as a library
You can use jadx in your java projects, check details on [wiki page](https://github.com/skylot/jadx/wiki/Use-jadx-as-a-library)

### Build from source
JDK 11 or higher must be installed:
```
git clone https://github.com/skylot/jadx.git
cd jadx
./gradlew dist
```

(on Windows, use `gradlew.bat` instead of `./gradlew`)

Scripts for run jadx will be placed in `build/jadx/bin`
and also packed to `build/jadx-<version>.zip`

### Usage
```
jadx[-gui] [command] [options] <input files> (.apk, .dex, .jar, .class, .smali, .zip, .aar, .arsc, .aab, .xapk, .jadx.kts)
commands (use '<command> --help' for command options):
  plugins	  - manage jadx plugins

options:
  -d, --output-dir                      - output directory
  -ds, --output-dir-src                 - output directory for sources
  -dr, --output-dir-res                 - output directory for resources
  -r, --no-res                          - do not decode resources
  -s, --no-src                          - do not decompile source code
  --single-class                        - decompile a single class, full name, raw or alias
  --single-class-output                 - file or dir for write if decompile a single class
  --output-format                       - can be 'java' or 'json', default: java
  -e, --export-gradle                   - save as android gradle project
  -j, --threads-count                   - processing threads count, default: 4
  -m, --decompilation-mode              - code output mode:
                                           'auto' - trying best options (default)
                                           'restructure' - restore code structure (normal java code)
                                           'simple' - simplified instructions (linear, with goto's)
                                           'fallback' - raw instructions without modifications
  --show-bad-code                       - show inconsistent code (incorrectly decompiled)
  --no-xml-pretty-print                 - do not prettify XML
  --no-imports                          - disable use of imports, always write entire package name
  --no-debug-info                       - disable debug info parsing and processing
  --add-debug-lines                     - add comments with debug line numbers if available
  --no-inline-anonymous                 - disable anonymous classes inline
  --no-inline-methods                   - disable methods inline
  --no-move-inner-classes               - disable move inner classes into parent
  --no-inline-kotlin-lambda             - disable inline for Kotlin lambdas
  --no-finally                          - don't extract finally block
  --no-restore-switch-over-string       - don't restore switch over string
  --no-replace-consts                   - don't replace constant value with matching constant field
  --escape-unicode                      - escape non latin characters in strings (with \u)
  --respect-bytecode-access-modifiers   - don't change original access modifiers
  --mappings-path                       - deobfuscation mappings file or directory. Allowed formats: Tiny and Tiny v2 (both '.tiny'), Enigma (.mapping) or Enigma directory
  --mappings-mode                       - set mode for handling the deobfuscation mapping file:
                                           'read' - just read, user can always save manually (default)
                                           'read-and-autosave-every-change' - read and autosave after every change
                                           'read-and-autosave-before-closing' - read and autosave before exiting the app or closing the project
                                           'ignore' - don't read or save (can be used to skip loading mapping files referenced in the project file)
  --deobf                               - activate deobfuscation
  --deobf-min                           - min length of name, renamed if shorter, default: 3
  --deobf-max                           - max length of name, renamed if longer, default: 64
  --deobf-whitelist                     - space separated list of classes (full name) and packages (ends with '.*') to exclude from deobfuscation, default: android.support.v4.* android.support.v7.* android.support.v4.os.* android.support.annotation.Px androidx.core.os.* androidx.annotation.Px
  --deobf-cfg-file                      - deobfuscation mappings file used for JADX auto-generated names (in the JOBF file format), default: same dir and name as input file with '.jobf' extension
  --deobf-cfg-file-mode                 - set mode for handling the JADX auto-generated names' deobfuscation map file:
                                           'read' - read if found, don't save (default)
                                           'read-or-save' - read if found, save otherwise (don't overwrite)
                                           'overwrite' - don't read, always save
                                           'ignore' - don't read and don't save
  --deobf-res-name-source               - better name source for resources:
                                           'auto' - automatically select best name (default)
                                           'resources' - use resources names
                                           'code' - use R class fields names
  --use-source-name-as-class-name-alias - use source name as class name alias:
                                           'always' - always use source name if it's available
                                           'if-better' - use source name if it seems better than the current one
                                           'never' - never use source name, even if it's available
  --use-kotlin-methods-for-var-names    - use kotlin intrinsic methods to rename variables, values: disable, apply, apply-and-hide, default: apply
  --rename-flags                        - fix options (comma-separated list of):
                                           'case' - fix case sensitivity issues (according to --fs-case-sensitive option),
                                           'valid' - rename java identifiers to make them valid,
                                           'printable' - remove non-printable chars from identifiers,
                                          or single 'none' - to disable all renames
                                          or single 'all' - to enable all (default)
  --integer-format                      - how integers are displayed:
                                           'auto' - automatically select (default)
                                           'decimal' - use decimal
                                           'hexadecimal' - use hexadecimal
  --fs-case-sensitive                   - treat filesystem as case sensitive, false by default
  --cfg                                 - save methods control flow graph to dot file
  --raw-cfg                             - save methods control flow graph (use raw instructions)
  -f, --fallback                        - set '--decompilation-mode' to 'fallback' (deprecated)
  --use-dx                              - use dx/d8 to convert java bytecode
  --comments-level                      - set code comments level, values: error, warn, info, debug, user-only, none, default: info
  --log-level                           - set log level, values: quiet, progress, error, warn, info, debug, default: progress
  -v, --verbose                         - verbose output (set --log-level to DEBUG)
  -q, --quiet                           - turn off output (set --log-level to QUIET)
  --version                             - print jadx version
  -h, --help                            - print this help

Plugin options (-P<name>=<value>):
  dex-input: Load .dex and .apk files
    - dex-input.verify-checksum         - verify dex file checksum before load, values: [yes, no], default: yes
  java-convert: Convert .class, .jar and .aar files to dex
    - java-convert.mode                 - convert mode, values: [dx, d8, both], default: both
    - java-convert.d8-desugar           - use desugar in d8, values: [yes, no], default: no
  kotlin-metadata: Use kotlin.Metadata annotation for code generation
    - kotlin-metadata.class-alias       - rename class alias, values: [yes, no], default: yes
    - kotlin-metadata.method-args       - rename function arguments, values: [yes, no], default: yes
    - kotlin-metadata.fields            - rename fields, values: [yes, no], default: yes
    - kotlin-metadata.companion         - rename companion object, values: [yes, no], default: yes
    - kotlin-metadata.data-class        - add data class modifier, values: [yes, no], default: yes
    - kotlin-metadata.to-string         - rename fields using toString, values: [yes, no], default: yes
    - kotlin-metadata.getters           - rename simple getters to field names, values: [yes, no], default: yes
  rename-mappings: various mappings support
    - rename-mappings.format            - mapping format, values: [AUTO, TINY_FILE, TINY_2_FILE, ENIGMA_FILE, ENIGMA_DIR, SRG_FILE, XSRG_FILE, JAM_FILE, CSRG_FILE, TSRG_FILE, TSRG_2_FILE, PROGUARD_FILE, RECAF_SIMPLE_FILE, JOBF_FILE], default: AUTO
    - rename-mappings.invert            - invert mapping on load, values: [yes, no], default: no
  smali-input: Load .smali files
    - smali-input.api-level             - Android API level, default: 27

Environment variables:
  JADX_DISABLE_XML_SECURITY - set to 'true' to disable all security checks for XML files
  JADX_DISABLE_ZIP_SECURITY - set to 'true' to disable all security checks for zip files
  JADX_ZIP_MAX_ENTRIES_COUNT - maximum allowed number of entries in zip files (default: 100 000)
  JADX_CONFIG_DIR - custom config directory, using system by default
  JADX_CACHE_DIR - custom cache directory, using system by default
  JADX_TMP_DIR - custom temp directory, using system by default

Examples:
  jadx -d out classes.dex
  jadx --rename-flags "none" classes.dex
  jadx --rename-flags "valid, printable" classes.dex
  jadx --log-level ERROR app.apk
  jadx -Pdex-input.verify-checksum=no app.apk
```
These options also work in jadx-gui running from command line and override options from preferences' dialog

### Troubleshooting
Please check wiki page [Troubleshooting Q&A](https://github.com/skylot/jadx/wiki/Troubleshooting-Q&A)

### Contributing
To support this project you can:
  - Post thoughts about new features/optimizations that important to you
  - Submit decompilation issues, please read before proceed: [Open issue](CONTRIBUTING.md#Open-Issue)
  - Open pull request, please follow these rules: [Pull Request Process](CONTRIBUTING.md#Pull-Request-Process)

---------------------------------------
*Licensed under the Apache 2.0 License*
