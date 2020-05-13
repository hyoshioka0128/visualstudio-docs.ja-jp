---
title: ResourcesGenerator タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- embedding resources into a .resources file [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild], parameters
ms.assetid: e782bbac-9ee6-472b-8171-3ee008c77b4e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b5aba45292aaa55a719eb19d6f0f6f115e8b477
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632512"
---
# <a name="resourcesgenerator-task"></a>ResourcesGenerator タスク

<xref:Microsoft.Build.Tasks.Windows.ResourcesGenerator> タスクによって、1 つ以上のリソース ( *.jpg*、 *.ico*、 *.bmp*、バイナリ形式の XAML、その他の種類の拡張子) が *.resources* ファイルに埋め込まれます。

## <a name="task-parameters"></a>タスク パラメーター

|パラメーター|説明|
|---------------|-----------------|
|`OutputPath`|必須の **String** 型のパラメーターです。<br /><br /> 出力ディレクトリのパスを指定します。 パスが絶対パスではない場合は、プロジェクトのルート ディレクトリに対する相対パスとして扱われます。|
|`OutputResourcesFile`|必須の **ITaskItem[]** 型の出力パラメーターです。<br /><br /> 生成される *.resources* ファイルのパスと名前を指定します。 パスが絶対パスではない場合、 *.resources* ファイルはプロジェクトのルート ディレクトリに対する相対パスに作成されます。|
|`ResourcesFiles`|必須の **ITaskItem[]** 型のパラメーターです。<br /><br /> 生成される *.resources* ファイルに埋め込まれる 1 つ以上のリソースを指定します。|

## <a name="example"></a>例

 1 つの *.bmp* リソースを持つ *.resources* ファイルを作成する例を次に示します。 *.bmp* リソースは、プロジェクトのルート ディレクトリを基準にした相対ディレクトリに生成されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.ResourcesGenerator"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="ResourcesGeneratorTask">
    <ResourcesGenerator
      ResourceFiles="Resource1.bmp"
      OutputPath="myresources"
      OutputResourcesFile="myresources\my.resources" />
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [WPF MSBuild のリファレンス](../msbuild/wpf-msbuild-reference.md)
- [タスク リファレンス](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [WPF アプリケーション (WPF) のビルド](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)