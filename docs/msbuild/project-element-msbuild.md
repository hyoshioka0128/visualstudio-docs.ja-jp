---
title: Project 要素 (MSBuild) | Microsoft Docs
description: MSBuild プロジェクト ファイルの必須ルート要素である MSBuild Project 要素について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Project
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ToolsVersion attribute [MSBuild]
- <Project> element [MSBuild]
- Project element [MSBuild]
ms.assetid: d1cda56a-dbef-4109-9201-39e962e3f653
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 223ccd9e823bef4ee458a7aa1ce2d785788c6238
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048856"
---
# <a name="project-element-msbuild"></a>Project 要素 (MSBuild)

MSBuild プロジェクト ファイルの必須のルート要素です。

## <a name="syntax"></a>構文

```xml
<Project InitialTargets="TargetA;TargetB"
         DefaultTargets="TargetC;TargetD"
         TreatAsLocalProperty="PropertyA;PropertyB"
         ToolsVersion=<version number>
         Sdk="name[/version]"
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Sdk... />
    <Choose>... </Choose>
    <PropertyGroup>... </PropertyGroup>
    <ItemGroup>... </ItemGroup>
    <Target>... </Target>
    <UsingTask.../>
    <ProjectExtensions>... </ProjectExtensions>
    <Import... />
</Project>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|------------------------| - |
| `DefaultTargets` | 省略可能な属性です。<br /><br /> ターゲットが指定されていない場合にビルドのエントリ ポイントとなる 1 つまたは複数の既定のターゲット。 複数のターゲットはセミコロン (;) で区切られます。<br /><br /> `DefaultTargets` 属性または MSBuild コマンド ラインのいずれかで既定のターゲットが指定されていない場合、[Import](../msbuild/import-element-msbuild.md) 要素の評価後、エンジンによってプロジェクト ファイルの最初のターゲットが実行されます。 |
| `InitialTargets` | 省略可能な属性です。<br /><br /> `DefaultTargets` 属性またはコマンド ラインで指定されたターゲットの前に実行される 1 つまたは複数の初期ターゲット。 複数のターゲットはセミコロン (`;`) で区切られます。 複数のインポートされたファイルで `InitialTargets` が定義されている場合は、記載されているすべてのターゲットが、インポートが発生する順序で実行されます。 |
| `Sdk` | 省略可能な属性です。 <br /><br /> .proj ファイルに追加される暗黙的なインポート ステートメントの作成に使用する SDK 名と省略可能なバージョン。 バージョンが指定されていない場合、MSBuild は、既定のバージョンを解決しようとします。  たとえば、`<Project Sdk="Microsoft.NET.Sdk" />` または `<Project Sdk="My.Custom.Sdk/1.0.0" />` です。 |
| `ToolsVersion` | 省略可能な属性です。<br /><br /> MSBuild が $(MSBuildBinPath) と $(MSBuildToolsPath) の値を決定するために使用するツールセットのバージョン。 |
| `TreatAsLocalProperty` | 省略可能な属性です。<br /><br /> グローバルとは見なされないプロパティ名。 この属性は、プロジェクトまたはターゲット ファイル、および後続のすべてのインポートに設定されているプロパティ値が特定のコマンド ライン プロパティによってオーバーライドされることを防ぎます。 複数のプロパティはセミコロン (;) で区切られます。<br /><br /> 通常、グローバル プロパティは、プロジェクト ファイルまたはターゲット ファイルで設定されたプロパティ値をオーバーライドします。 プロパティが `TreatAsLocalProperty` 値に一覧表示されている場合、グローバル プロパティ値は、そのファイルと後続のインポートに設定されているプロパティ値をオーバーライドしません。 詳細については、「[方法:同じソース ファイルを異なるオプションでビルドする](../msbuild/how-to-build-the-same-source-files-with-different-options.md)」を参照してください。 **注:**  グローバル プロパティは、コマンド プロンプトで **-property** (または **-p** ) スイッチを使用して設定します。 また、複数プロジェクト ビルドの子プロジェクトのグローバル プロパティは、MSBuild タスクの `Properties` 属性を使用して設定または変更することもできます。 詳細については、「[MSBuild タスク](../msbuild/msbuild-task.md)」を参照してください。 |
| `xmlns` | 省略可能な属性です。<br /><br /> `xmlns` 属性には、"`http://schemas.microsoft.com/developer/msbuild/2003`" の値を指定する必要があります。 |

### <a name="child-elements"></a>子要素

| 要素 | 説明 |
| - | - |
| [Choose](../msbuild/choose-element-msbuild.md) | 省略可能な要素です。<br /><br /> 子要素を評価して、`ItemGroup` 要素および/または `PropertyGroup` 要素の 1 つのセットを評価対象に選択します。 |
| [[インポート]](../msbuild/import-element-msbuild.md) | 省略可能な要素です。<br /><br /> プロジェクト ファイルが別のプロジェクト ファイルをインポートできるようにします。 1 つのプロジェクトに 0 個以上の `Import` 要素を含めることができます。 |
| [ImportGroup](../msbuild/importgroup-element.md) | 省略可能な要素です。<br /><br /> オプションの条件下でグループ化された `Import` 要素のコレクションが格納されます。 |
| [ItemGroup](../msbuild/itemgroup-element-msbuild.md) | 省略可能な要素です。<br /><br /> 個々の項目の grouping 要素。 項目は [Item](../msbuild/item-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `ItemGroup` 要素を含めることができます。 |
| [ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md) | 省略可能な要素です。<br /><br /> 一連の項目定義を定義できます。これは、プロジェクト内のすべての項目に既定で適用されるメタデータ値です。 ItemDefinitionGroup は、`CreateItem` タスクおよび `CreateProperty` タスクを使用する必要性より優先されます。 |
| [ProjectExtensions](../msbuild/projectextensions-element-msbuild.md) | 省略可能な要素です。<br /><br /> MSBuild プロジェクト ファイルに MSBuild 以外の情報を保持する方法を提供します。 1 つのプロジェクトに 0 個または 1 個の `ProjectExtensions` 要素を含めることができます。 |
| [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) | 省略可能な要素です。<br /><br /> 個々のプロパティの grouping 要素。 プロパティは [Property](../msbuild/property-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `PropertyGroup` 要素を含めることができます。 |
| [Sdk](../msbuild/sdk-element-msbuild.md) | 省略可能な要素です。<br /><br /> MSBuild プロジェクト SDK が参照されます。  この要素は、Sdk 属性の代わりとして使用できます。 |
| [移行先](../msbuild/target-element-msbuild.md) | 省略可能な要素です。<br /><br /> MSBuild によって順次実行されるタスクのセットを格納します。 タスクは [Task](../msbuild/task-element-msbuild.md) 要素を使用して指定されます。 1 つのプロジェクトに 0 個以上の `Target` 要素を含めることができます。 |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | 省略可能な要素です。<br /><br /> MSBuild でタスクを登録する方法を指定します。 1 つのプロジェクトに 0 個以上の `UsingTask` 要素を含めることができます。 |

### <a name="parent-elements"></a>親要素

 [なし] :

## <a name="see-also"></a>関連項目

- [方法: 最初にビルドするターゲットを指定する](../msbuild/how-to-specify-which-target-to-build-first.md)
- [コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild](../msbuild/msbuild.md)
