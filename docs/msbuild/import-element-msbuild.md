---
title: Import 要素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Import
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Import element [MSBuild]
- <Import> element [MSBuild]
ms.assetid: 3bfecaf1-69fd-4008-b651-c9dafd4389d9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 044c531432de987fc7f3d34ce5344ad0374bcd00
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633747"
---
# <a name="import-element-msbuild"></a>Import 要素 (MSBuild)

1 つのプロジェクト ファイルの内容を別のプロジェクト ファイルにインポートします。

\<Project> \<Import>

## <a name="syntax"></a>構文

```xml
<Import Project="ProjectPath"
    Condition="'String A'=='String B'" />
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Project`|必須の属性です。<br /><br /> インポートするプロジェクト ファイルのパス。 パスにはワイルドカードを含めることができます。 一致するファイルは、並べ替えられた順にインポートされます。 この機能を使用すると、コード ファイルをディレクトリに追加するだけで、プロジェクトにコードを追加できます。|
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|
|`Sdk`| 省略可能な属性です。<br /><br /> プロジェクト SDK を参照します。|

### <a name="child-elements"></a>子要素

 None

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |
| [ImportGroup](../msbuild/importgroup-element.md) | オプションの条件下でグループ化された `Import` 要素のコレクションが格納されます。 |

## <a name="remarks"></a>Remarks

 `Import` 要素を使用すると、複数のプロジェクト ファイルに共通するコードを再利用できます。 これにより、共有されたコードに対する更新が、そのコードをインポートしたすべてのプロジェクトに反映されるため、コードの保守が容易になります。

 規則により、インポートされた共有プロジェクト ファイルは *.targets* ファイルとして保存されますが、これらは標準の MSBuild プロジェクト ファイルです。 MSBuild では、別のファイル名拡張子を持つプロジェクトをインポートすることもできますが、一貫性のために *.targets* 拡張子を使用することをお勧めします。

 インポートされるプロジェクト内の相対パスは、インポートする側のプロジェクトのディレクトリからの相対パスであると解釈されます。 したがって、あるプロジェクト ファイルを別々の場所に存在する複数のプロジェクト ファイルにインポートする場合、インポートされるプロジェクト ファイル内の相対パスは、インポートされるプロジェクトごとに異なって解釈されます。

 MSBuild で予約されている、プロジェクト ファイル関連の全プロパティ (例: `MSBuildProjectDirectory`、`MSBuildProjectFile`) は、インポートされたプロジェクトで参照される場合、インポートするプロジェクト ファイルに基づいて値が割り当てられます。

 インポートされるプロジェクトに `DefaultTargets` 属性がない場合は、インポートされる各プロジェクトがインポート順にチェックされ、最初に検出された `DefaultTargets` 属性の値が使用されます。 たとえば、ProjectA で ProjectB と ProjectC を (この順序で) インポートし、ProjectB で ProjectD をインポートする場合、MSBuild では、ProjectA、ProjectB、ProjectD、ProjectC の順序で指定された `DefaultTargets` が検索されます。

 インポートされるプロジェクトのスキーマは、標準プロジェクトのスキーマと同じです。 MSBuild では、インポートされたプロジェクトをビルドできる場合もありますが、インポートされたプロジェクトには、設定するプロパティやターゲットを実行する順序に関する情報が通常は含まれていないため、ビルドできる可能性は低くなります。 インポートされるプロジェクトのこれらの情報は、インポートするプロジェクトに依存します。

## <a name="wildcards"></a>ワイルドカード

 .NET Framework 4 では、MSBuild で、Project 属性でのワイルドカードが許可されます。 ワイルドカードがある場合、見つかったすべての一致が並べ替えられ (再現可能性の確保のため)、順序が明示的に設定されていたかのように、その順序でインポートされます。

 これは、機能拡張ポイントを提供して、自身がファイル名をインポート対象のファイルに明示的に追加しなくても、他のユーザーがファイルをインポートできるようにする場合に便利です。 このために、*Microsoft.Common.Targets* ではファイルの先頭に次の行が含まれています。

```xml
<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore\*" Condition="'$(ImportByWildcardBeforeMicrosoftCommonTargets)' == 'true' and exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore')"/>
```

## <a name="example"></a>例

 次の例は、いくつかの項目やプロパティがあり、一般的なプロジェクト ファイルをインポートするプロジェクトを示しています。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <resourcefile>Strings.resx</resourcefile>

        <compiledresources>
            $(O)\$(MSBuildProjectName).Strings.resources
        </compiledresources>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="*.cs" />

        <Reference Include="System" />
        <Reference Include="System.Data" />
    </ItemGroup>

    <Import Project="$(CommonLocation)\General.targets" />
</Project>
```

## <a name="see-also"></a>関連項目

- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
- [方法: 複数のプロジェクト ファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
