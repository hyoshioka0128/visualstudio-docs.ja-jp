---
title: UidManager タスク | Microsoft Docs
description: MSBuild UidManager タスクで、一意識別子 (UID) をチェック、更新、または削除して、ソース XAML ファイル内のすべての XAML 要素をローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UidManager task [WPF MSBuild]
- UidManager task [WPF MSBuild], parameters
- managing UIDs when localizing XAML elements [WPF MSBuild]
- localizing XAML elements [WPF MSBuild], managing UIDs
- checking UIDs when localizing XAML elements [WPF MSBuild]
ms.assetid: 4fc7b5a5-11b0-46ca-9656-8c2a0b08d1fe
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 852b910de742676e1fe7dd0c85129640eb37a9ae
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046933"
---
# <a name="uidmanager-task"></a>UidManager タスク

ソース XAML ファイルに含まれるすべての XAML 要素をローカライズするために、<xref:Microsoft.Build.Tasks.Windows.UidManager> タスクによって一意識別子 (UID) のチェック、更新、または削除が行われます。

## <a name="task-parameters"></a>タスク パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `IntermediateDirectory` | 省略可能な **String** 型のパラメーターです。<br /><br /> **MarkupFiles** パラメーターで指定されるソース XAML ファイルをバックアップするために使用されるディレクトリを指定します。 |
| `MarkupFiles` | 必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> UID のチェック、更新、または削除のために含めるソース XAML ファイルを指定します。 |
| `Task` | 必須の **String** 型のパラメーターです。<br /><br /> 実行する UID 管理タスクを指定します。 有効なオプションは **Check** 、 **Update** 、または **Remove** です。 |

## <a name="example"></a>例

 次の例では <xref:Microsoft.Build.Tasks.Windows.UidManager> タスクを使用して、指定されたソース XAML ファイルに、適切な UID を持つ XAML 要素が含まれていることをチェックします。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.UidManager"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="UidManagerTask">
    <UidManager
      Task="Check"
      MarkupFiles="Page1.xaml;Page2.xaml"
      IntermediateDirectory="c:\UidManagerIntermediateDirectory" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [方法: アプリケーションをローカライズする](/dotnet/framework/wpf/advanced/how-to-localize-an-application)