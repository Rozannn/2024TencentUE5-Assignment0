# 2024TencentUE5-Assignment0

### 编译UE5源码

编译后并创建第一人称射击模板C++项目

![Fig1]([img\Fig1.png](https://github.com/Rozannn/2024TencentUE5-Assignment0/blob/main/img/Fig1.png))

将UnrealEditor.exe附加到进程即可在创建项目后自动在引擎中打开

![Fig2](img\Fig2.png)

### 打包安卓项目

使用UE自带的Turkey自动配置Android Studio环境，仅需要手动选择SDK进行安装

打包安装后出现permission required youmust approve this permission in app settin:storage，但app未申请权限，导致只能点击quit。通过取消项目设置中的show launch image能够取消弹窗，但无法解决权限问题。

造成原因为Android13 (sdk33) 细化了外部存储权限，导致原本的请求方式失效。

#### 解决方案一

将UEDeployAndroid.cs中如下代码段if中的代码注释掉，即不再请求存储权限。

```c++
// Figure out the required startup permissions if targetting devices supporting runtime permissions
String StartupPermissions = "";
if (TargetSDKVersion >= 23)
{
    if (Configuration != "Shipping" || !bUseExternalFilesDir)
    {
        StartupPermissions = StartupPermissions + (StartupPermissions.Length > 0 ? "," : "") + "android.permission.WRITE_EXTERNAL_STORAGE";
    }
}
```

#### 解决方法二

将SDK版本更改到33以下。

#### 解决方法三

在项目设置中添加如下三条Extra Permissions

![Fig3](img\Fig3.png)

打包后的游戏运行视频为演示视频.mp4

![Fig4](C:\UE_ASSIGNMENT\2024TencentUE5-Assignment0\img\Fig4.png)





