---
title: MergeLocalizationDirectives タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- localizing XAML [WPF MSBuild], moving comments and attributes to a separate file
- MergeLocalizationDirectives task [WPF MSBuild], parameters
- MergeLocalizationDirectives task [WPF MSBuild]
- moving localization comments and attributes to a separate file [WPF MSBuild]
ms.assetid: 9095b4f1-88da-4194-914b-ee1456826830
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c7699afeb09604a437aad091f9aaf9ce624d33e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633500"
---
# <a name="mergelocalizationdirectives-task"></a>MergeLocalizationDirectives タスク

<xref:Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives> タスクは、1 つ以上の XAML バイナリ形式ファイルのローカリゼーション属性とコメントを、アセンブリ全体で単一のファイルにマージします。

## <a name="task-parameters"></a>タスク パラメーター

| パラメーター | 説明 |
|------------------------------| - |
| `GeneratedLocalizationFiles` | 必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> XAML バイナリ形式の個々のファイルに対するローカリゼーション ディレクティブ ファイルの一覧を指定します。 |
| `OutputFile` | 省略可能な **String** 型の出力パラメーターです。<br /><br /> コンパイルされたローカリゼーション ディレクティブ アセンブリの出力パスを指定します。 |

## <a name="remarks"></a>Remarks

XAML のコンテンツには、ローカリゼーション属性とコメントを追加できます。 Windows Presentation Foundation (WPF) のローカリゼーション サポートを使用すると、ローカリゼーション属性とコメントを取り出し、生成されるアセンブリとは別の *.loc* ファイルに格納できます。 これを行うには、**LocalizationPropertyStorage** 属性を使用します。 ローカリゼーション属性とコメント、および **LocalizationPropertyStorage** の詳細については、「[ローカリゼーション属性とコメント](/dotnet/framework/wpf/advanced/localization-attributes-and-comments)」を参照してください。

## <a name="example"></a>例

いくつかの XAML バイナリ形式ファイルのローカリゼーション コメントを単一の *.loc* ファイルにマージする方法を次の例に示します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="MergeLocalizationDirectivesTask">
    <MergeLocalizationDirectives
      GeneratedLocalizationFiles="obj\debug\page1.loc;obj\debug\page2.loc;obj\debug\page3.loc"
      OutputFile="obj\debug\WPFMSBuildSample.loc" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [WPF MSBuild タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [MSBuild タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
