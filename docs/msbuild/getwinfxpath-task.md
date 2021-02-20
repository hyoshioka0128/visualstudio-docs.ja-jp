---
title: GetWinFXPath タスク | Microsoft Docs
description: 現在の .NET ランタイムのディレクトリが返される、MSBuild GetWinFXPath タスクを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- getting the directory of the current .NET Framework runtime [WPF MSBuild]
- GetWinFXPath task [WPF MSBuild], parameters
- GetWinFXPath task [WPF MSBuild]
- obtaining the path to the current .NET Framework runtime [WPF MSBuild]
ms.assetid: b1dfb467-f3d3-47f3-83ef-af7b0e33a772
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 164f9f91eda1d81db00d25bb4e18a6cbb352e41e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914625"
---
# <a name="getwinfxpath-task"></a>GetWinFXPath タスク

<xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> タスクを実行すると、現在の .NET ランタイムのディレクトリが返されます。

## <a name="task-parameters"></a>タスク パラメーター

| パラメーター | 説明 |
|-------------------| - |
| `WinFXPath` | 省略可能な **String** 型の出力パラメーターです。<br /><br /> .NET ランタイムへの実際のパスを指定します。 |
| `WinFXNativePath` | 必須の **String** 型のパラメーターです。<br /><br /> ネイティブ .NET ランタイムへのパスを指定します。 |
| `WinFXWowPath` | 必須の **String** 型のパラメーターです。<br /><br /> 64 ビット システム上の 32 ビット **Windows on Windows** モジュール内の .NET アセンブリへのパスを指定します。 |

## <a name="remarks"></a>解説

 <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> タスクが 64 ビット プロセッサで実行されている場合、**WinFXPath** パラメーターは **WinFXWowPath** パラメーターに保存されているパスに設定されます。それ以外の場合、**WinFXPath** パラメーターは **WinFXNativePath** パラメーターに保存されているパスに設定されます。

## <a name="example"></a>例

 次の例では、**GetWinFXPath** タスクを使用して、.NET ランタイムへのネイティブ パスを検出する方法を示します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.GetWinFXPath"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="GetWinFXPathTask">
    <GetWinFXPath
      WinFXNativePath="c:\WinFXNative"
      WinFXWowPath="c:\WinFXWowNative" />
  </Target>
  <Import Project="$(MSBuildBinPath)\Microsoft.WinFX.targets" />
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
