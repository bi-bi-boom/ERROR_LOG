---
title: iOS 检测第一次 / 新版本第一次进入 App
date: 2020-11-09 10:21:55
categories: 
  - [iOS, 实用]
tags:
  - "author: cloxnu"
  - Swift
  - Objective-C
---

项目中经常需要检测应用是否第一次打开，判断是否需要新手引导，将检测代码写在另一个 class 的静态方法中，再在需要的页面或 AppDelegate 中调用。

<!-- More -->

Swift:

```swift
// 检测第一次打开
static func isFirstLaunch() -> Bool {
    let isFirstLaunch = !UserDefaults.standard.bool(forKey: "hasBeenLaunched")
    if isFirstLaunch
    {
        UserDefaults.standard.set(true, forKey: "hasBeenLaunched")
    }
    return isFirstLaunch
}

// 检测第一次打开 / 新版本第一次打开
static func isFirstLaunchOfNewVersion() -> Bool {
    let defaults = UserDefaults.standard;
    let currentVersion = Bundle.main.infoDictionary!["CFBundleShortVersionString"] as! String
    let lastLaunchVersion = defaults.string(forKey: "lastLaunchVersion")
    if (!lastLaunchVersion) {
        // 第一次打开
        defaults.set(currentVersion, forKey: "lastLaunchVersion")
        return true
    }
    else if (lastLaunchVersion != currentVersion) {
        // 版本更新第一次打开
        defaults.set(currentVersion, forKey: "lastLaunchVersion")
        return true
    }
    return false
}

// 检测某个页面是否第一次打开 / 新版本第一次打开（需要传递 classname）
static func isFirstLaunchOfNewVersion(inClassName name: String) {
    let defaults = UserDefaults.standard;
    let currentVersion = Bundle.main.infoDictionary!["CFBundleShortVersionString"] as! String
    let lastLaunchVersion = defaults.string(forKey: "lastLaunchVersion_" + name)
    if (!lastLaunchVersion) {
        // 第一次打开
        defaults.set(currentVersion, forKey: "lastLaunchVersion_" + name)
        return true
    }
    else if (lastLaunchVersion != currentVersion) {
        // 版本更新第一次打开
        defaults.set(currentVersion, forKey: "lastLaunchVersion_" + name)
        return true
    }
    return false
}
```

对于检测某个页面是否第一次打开只需在目标 ViewController 里加上

```swift
if (isFirstLaunchOfNewVersion(inClassName: String(describing: self.classForCoder))) {
    // print("第一次打开，启动新手引导")
}
```

Objective-C:

```objc
+ (BOOL) isFirstLaunch {
    BOOL isFirstLaunch = ![[NSUserDefaults standardUserDefaults] boolForKey:@"hasBeenLaunched"];
    if (isFirstLaunch) {
        [[NSUserDefaults standardUserDefaults] setBool:YES forKey:@"hasBeenLaunched"];
    }
    return isFirstLaunch;
}

+ (BOOL) isFirstLaunchOfNewVersion {
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    NSString *currentVersion = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"];
    NSString *lastLaunchVersion = [defaults objectForKey:@"lastLaunchVersion"];
    if (!lastLaunchVersion) {
        // 第一次打开
        [defaults setObject:currentVersion forKey:@"lastLaunchVersion"];
        return YES;
    }
    else if (![lastLaunchVersion isEqualToString:currentVersion]) {
        // 版本更新第一次打开
        [defaults setObject:currentVersion forKey:@"lastLaunchVersion"];
        return YES;
    }
    return NO;
}

+ (BOOL) isFirstLaunchOfNewVersionInClassName:(NSString *)name {
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
    NSString *currentVersion = [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"];
    NSString *lastLaunchVersion = [defaults objectForKey:[@"lastLaunchVersion_" stringByAppendingString:name]];
    if (!lastLaunchVersion) {
        // 第一次打开
        [defaults setObject:currentVersion forKey:[@"lastLaunchVersion_" stringByAppendingString:name]];
        return YES;
    }
    else if (![lastLaunchVersion isEqualToString:currentVersion]) {
        // 版本更新第一次打开
        [defaults setObject:currentVersion forKey:[@"lastLaunchVersion_" stringByAppendingString:name]];
        return YES;
    }
    return NO;
}
```

对于检测某个页面是否第一次打开只需在目标 ViewController 里加上

```objc
if (isFirstLaunchOfNewVersionInClassName:NSStringFromClass([self class])) {
    // print("第一次打开，启动新手引导")
}
```
