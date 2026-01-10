---
title: fnm Windows 安装指南
tags: [fnm]
updated: 2026-01-04
---

---

## 介绍

fnm (Fast Node Manager) ，快速简便的 No​​de.js 版本管理器，使用 Rust 构建，类似于 nvm，但它更快且易于使用。

## 步骤

1. 使用`winget`安装fnm：(假设我需要自定义安装在D:\Dev\fnm目录下)

   ```powershell
   winget install Schniz.fnm -l "D:\Dev\fnm"
   ```

2. 修改powershell配置

   找到powershell配置文件，可能在：

   * `%userprofile%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1` Powershell 5
   * `%userprofile%\Documents\PowerShell\Microsoft.PowerShell_profile.ps1` Powershell 6+
  
   作者的配置文件是在第一条的位置，名字不必一模一样，比如作者的是`profile.ps1`

   在文件末尾添加以下内容：

   ```powershell
   fnm env --use-on-cd --shell powershell | Out-String | Invoke-Expression
   ```

3. 修改环境变量

   这里我们要自定义`nodejs`的安装目录，我们假设想安装在`D:\Dev\fnm\fnm_node_versions`目录下

   首先我们在`D:\Dev\fnm`目录下创建`fnm_node_versions`文件夹

   然后按Windows徽标键，搜索`env`，选择`编辑系统环境变量`，然后点击`环境变量(N)...`按钮

   在用户变量区域，点击新建，变量名填写`FNM_DIR`，变量值填写`D:\Dev\fnm\fnm_node_versions`

   一路确定保存

4. 重启powershell，验证安装

   ```powershell
    fnm --version
   ```

   会出现类似以下信息，即表示安装成功

    ```powershell
    fnm 1.38.1
    ```

5. 更改安装目录权限

   在文件管理器中打开`D:\Dev`目录，找到`fnm`文件夹，右键点击选择`属性`，然后选择`安全`选项卡，点击`编辑...`按钮，将所有出现的用户的所有权限（除了特殊权限）勾选为允许，一路点击确定

6. 使用fnm安装nodejs

   ```powershell
   # 安装nodejs 24版本
   fnm install 24
   # 切换到nodejs 24版本
   fnm use 24
   # 设置默认版本为nodejs 24
   fnm default 24
   ```

   验证nodejs安装成功

   ```powershell
   node -v
   ```

   会出现类似以下信息，即表示安装成功

   ```powershell
   v24.12.0
   ```

## 参考

* [fnm 官方文档](https://github.com/Schniz/fnm/blob/master/README.md)
