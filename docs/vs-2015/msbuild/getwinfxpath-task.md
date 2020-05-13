---
title: GetWinFXPath タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: da32f0bfce9edf652e19df6b68bc51ed92624d80
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699005"
---
# <a name="getwinfxpath-task"></a>GetWinFXPath タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> タスクは、現在の [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] ランタイムのディレクトリを返します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`WinFXPath`|省略可能な **String** 型の出力パラメーターです。<br /><br /> [!INCLUDE[TLA2#tla_winfx](../includes/tla2sharptla-winfx-md.md)] ランタイムへの実際のパスを指定します。|  
|`WinFXNativePath`|必須の **String** 型のパラメーターです。<br /><br /> ネイティブ [!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)] ランタイムへのパスを指定します。|  
|`WinFXWowPath`|必須の **String** 型のパラメーターです。<br /><br /> 64 ビット システムの 32 ビット **Windows on Windows** モジュール内の [!INCLUDE[TLA#tla_winfx](../includes/tlasharptla-winfx-md.md)] アセンブリへのパスを指定します。|  
  
## <a name="remarks"></a>解説  
 <xref:Microsoft.Build.Tasks.Windows.GetWinFXPath> タスクが 64 ビット プロセッサで実行されている場合、**WinFXPath** パラメーターは **WinFXWowPath** パラメーターに保存されているパスに設定されます。それ以外の場合、**WinFXPath** パラメーターは **WinFXNativePath** パラメーターに保存されているパスに設定されます。  
  
## <a name="example"></a>例  
 次の例では、**GetWinFXPath** タスクを使用して、[!INCLUDE[TLA2#tla_titlewinfx](../includes/tla2sharptla-titlewinfx-md.md)] ランタイムへのネイティブ パスを検出する方法を示します。  
  
```  
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
 [WPF MSBuild リファレンス](../msbuild/wpf-msbuild-reference.md)   
 [Task Reference (タスク リファレンス)](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [WPF アプリケーション (WPF) のビルド](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)
