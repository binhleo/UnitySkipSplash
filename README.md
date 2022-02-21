[(English)](README_EN.md)

# UnitySkipSplash

## 简介
- 一个脚本跳过 Unity Logo 闪屏界面。

## 使用方法
- 需要 Unity2019.4 或更高版本。
- 将 [`SkipSplash.cs`](https://github.com/psygames/UnitySkipSplash/blob/main/SkipSplash.cs) 放到你的项目任意目录下（ `Editor` 除外）。
- 完成，打包APP尽情享用吧~

## 全部代码
```csharp
/* ---------------------------------------------------------------- */
/*                    Skip Unity Splash Screen                      */
/*                      Create by psygames                          */
/*            https://github.com/psygames/UnitySkipSplash           */
/* ---------------------------------------------------------------- */

#if !UNITY_EDITOR
using UnityEngine;
using UnityEngine.Rendering;

public class SkipSplash
{
    [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSplashScreen)]
    private static void BeforeSplashScreen()
    {
#if UNITY_WEBGL
        Application.focusChanged += Application_focusChanged;
#else
        System.Threading.Tasks.Task.Run(AsyncSkip);
#endif
    }

#if UNITY_WEBGL
    private static void Application_focusChanged(bool obj)
    {
        Application.focusChanged -= Application_focusChanged;
        SplashScreen.Stop(SplashScreen.StopBehavior.StopImmediate);
    }
#else
    private static void AsyncSkip()
    {
        SplashScreen.Stop(SplashScreen.StopBehavior.StopImmediate);
    }
#endif
}
#endif
```
