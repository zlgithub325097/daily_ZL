### IOS 集成 React-native pod 报错

    jonsondeMacBook-Pro:XXX jonsonliu$ pod install
    Analyzing dependencies
    Fetching podspec for `React` from `../node_modules/react-native`
    Fetching podspec for `glog` from `../node_modules/react-native/third-party-podspecs/glog.podspec`
    Fetching podspec for `yoga` from `../node_modules/react-native/ReactCommon/yoga`
    Downloading dependencies
    Using AFNetworking (3.2.0)
    Using Base64nl (1.2)
    Installing DoubleConversion (1.1.5)
    Using FSCalendar (2.7.9)
    Installing Folly (2016.09.26.00)
    Using IQKeyboardManager (5.0.7)
    Using M13BadgeView (1.0.4)
    Using MBProgressHUD (1.1.0)
    Using MJExtension (3.0.13)
    Using MJRefresh (3.1.15.3)
    Installing React (0.55.4)
    Using ReactiveObjC (3.0.0)
    Using SDWebImage (4.3.0)
    Using UITextView+Placeholder (1.2.0)
    Installing boost-for-react-native (1.63.0)
    Installing glog (0.3.4)
    [!] /bin/bash -c 
    set -e
    #!/bin/bash
    set -e

    PLATFORM_NAME="${PLATFORM_NAME:-iphoneos}"
    CURRENT_ARCH="${CURRENT_ARCH:-armv7}"

    export CC="$(xcrun -find -sdk $PLATFORM_NAME cc) -arch $CURRENT_ARCH -isysroot $(xcrun -sdk $PLATFORM_NAME --show-sdk-path)"
    export CXX="$CC"

    # Remove automake symlink if it exists
    if [ -h "test-driver" ]; then
        rm test-driver
    fi

    ./configure --host arm-apple-darwin

    # Fix build for tvOS
    cat << EOF >> src/config.h

    /* Add in so we have Apple Target Conditionals */
    #ifdef __APPLE__
    #include <TargetConditionals.h>
    #include <Availability.h>
    #endif

    /* Special configuration for AppleTVOS */
    #if TARGET_OS_TV
    #undef HAVE_SYSCALL_H
    #undef HAVE_SYS_SYSCALL_H
    #undef OS_MACOSX
    #endif

    /* Special configuration for ucontext */
    #undef HAVE_UCONTEXT_H
    #undef PC_FROM_UCONTEXT
    #if defined(__x86_64__)
    #define PC_FROM_UCONTEXT uc_mcontext->__ss.__rip
    #elif defined(__i386__)
    #define PC_FROM_UCONTEXT uc_mcontext->__ss.__eip
    #endif
    EOF

    checking for a BSD-compatible install... /usr/bin/install -c
    checking whether build environment is sane... yes
    checking for arm-apple-darwin-strip... no
    checking for strip... strip
    checking for a thread-safe mkdir -p... ./install-sh -c -d
    checking for gawk... no
    checking for mawk... no
    checking for nawk... no
    checking for awk... awk
    checking whether make sets $(MAKE)... yes
    checking whether make supports nested variables... yes
    checking for arm-apple-darwin-gcc... /Library/Developer/CommandLineTools/usr/bin/cc -arch armv7 -isysroot 
    checking whether the C compiler works... no
    xcrun: error: SDK "iphoneos" cannot be located
    xcrun: error: SDK "iphoneos" cannot be located
    xcrun: error: SDK "iphoneos" cannot be located
    xcrun: error: unable to lookup item 'Path' in SDK 'iphoneos'
    /Users/jonsonliu/Library/Caches/CocoaPods/Pods/External/glog/f09d6cdb8398b4922e87d51f5245de7e-1de0b/missing: Unknown `--is-lightweight' option
    Try `/Users/jonsonliu/Library/Caches/CocoaPods/Pods/External/glog/f09d6cdb8398b4922e87d51f5245de7e-1de0b/missing --help' for more information
    configure: WARNING: 'missing' script is too old or missing
    configure: error: in `/Users/jonsonliu/Library/Caches/CocoaPods/Pods/External/glog/f09d6cdb8398b4922e87d51f5245de7e-1de0b':
    configure: error: C compiler cannot create executables
    See `config.log' for more details


    [!] Smart quotes were detected and ignored in your Podfile. To avoid issues in the future, you should not use TextEdit for editing it. If you are not using TextEdit, you should turn off smart quotes in your editor of choice.

处理方案:    sudo xcode-select --switch/Applications/Xcode.app

文章链接:[https://www.jianshu.com/p/cbf22dcae059](https://www.jianshu.com/p/cbf22dcae059)

### IOS 导入Pods报错

```
diff: /../Podfile.lock: No such file or directory   
diff: /Manifest.lock: No such file or directory error: The sandbox is not in sync with the Podfile.lock. 
Run 'pod install' or update your CocoaPods installation.
```

解决方案

```
1> 删除四个文件：mingonghui.xcworkspace；Podfile；Podfile.lock；Pods
2> mingonghui.xcodeproj显示包内容，删除project.xcworkspace文件；
   返回项目根目录，打开原来后缀为xcodeproj的工程，可能会报错，接下来继续步骤。
3> 在target - Build Phases 中删除带有pod的项
```

截图如下:

![](/assets/1767501-46ac767b61cfde73.png)

```
4> 如果到这一步报错
   ld: library not found for -lPods-haoshuTest
   clang: error: linker command failed with exit code 1 (use -v to see invocation)
   删除爆红的静态库文件，编译就ok
```

截图如下:

![](/assets/2.png)

```
5> 最后，如果还有错误，可以尝试在工
```



