---
title: Import 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
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
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9f8edefc8e097f7ada67041b807231f594774548
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433549"
---
# <a name="import-element-msbuild"></a>Import 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

1 つのプロジェクト ファイルの内容を別のプロジェクト ファイルにインポートします。  
  
 \<Project>  
 \<Import>  
  
## <a name="syntax"></a>構文  
  
```  
<Import Project="ProjectPath"  
    Condition="'String A'=='String B'" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Project`|必須の属性です。<br /><br /> インポートするプロジェクト ファイルのパス。 パスにはワイルドカードを含めることができます。 一致するファイルは、並べ替えられた順にインポートされます。 この機能を使用すると、コード ファイルをディレクトリに追加するだけで、プロジェクトにコードを追加できます。|  
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[プロジェクト](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルの必須のルート要素です。|  
|[ImportGroup](../msbuild/importgroup-element.md)|オプションの条件下でグループ化された `Import` 要素のコレクションが格納されます。|  
  
## <a name="remarks"></a>Remarks  
 `Import` 要素を使用すると、複数のプロジェクト ファイルに共通するコードを再利用できます。 これにより、共有されたコードに対する更新が、そのコードをインポートしたすべてのプロジェクトに反映されるため、コードの保守が容易になります。  
  
 慣例により、インポートされた共有プロジェクト ファイルは .targets ファイルとして保存されますが、これらは標準の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルです。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、別のファイル名拡張子を使用してプロジェクトをインポートすることもできますが、一貫性を持たせるために .targets 拡張子を使用することをお勧めします。  
  
 インポートされるプロジェクト内の相対パスは、インポートする側のプロジェクトのディレクトリからの相対パスであると解釈されます。 したがって、あるプロジェクト ファイルを別々の場所に存在する複数のプロジェクト ファイルにインポートする場合、インポートされるプロジェクト ファイル内の相対パスは、インポートされるプロジェクトごとに異なって解釈されます。  
  
 `MSBuildProjectDirectory`、`MSBuildProjectFile` など、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] で予約されている全プロパティは、プロジェクト ファイルに関連し、インポートされるプロジェクトで参照されますが、これらにはインポートするプロジェクト ファイルに基づいた値が代入されます。  
  
 インポートされるプロジェクトに `DefaultTargets` 属性がない場合は、インポートされる各プロジェクトがインポート順にチェックされ、最初に検出された `DefaultTargets` 属性の値が使用されます。 たとえば、ProjectA で ProjectB および ProjectC を順番にインポートし、ProjectB で ProjectD をインポートする場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、ProjectA、ProjectB、ProjectD、ProjectC の順に `DefaultTargets` を検索します。  
  
 インポートされるプロジェクトのスキーマは、標準プロジェクトのスキーマと同じです。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] で、インポートされるプロジェクトをビルドできる場合もありますが、インポートされるプロジェクトには、設定するプロパティやターゲットを実行する順序に関する情報が通常は含まれていないため、ビルドできる可能性は低くなります。 インポートされるプロジェクトのこれらの情報は、インポートするプロジェクトに依存します。  
  
> [!NOTE]
> 条件付き import ステートメントがコマンド ライン MSBuilds で動作するときは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE) の MSBuilds とは連携しません。 条件付きインポートは、プロジェクトを読み込むときに設定される構成およびプラットフォームの値を使用して評価されます。 その後、プロジェクト ファイルでの条件の再評価が必要となる変更 (プラットフォームの変更など) が加えられると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はプロパティと項目の条件を再評価します。ただし、インポートの条件の再評価は行いません。 インポート条件は再評価されないため、インポートはスキップされます。  
>   
> このような状況が発生することを回避するには、.targets ファイルに条件付き import ステートメントを配置するか、または [Choose Element (MSBuild)](../msbuild/choose-element-msbuild.md) ブロックなどの条件付きブロックにコードを配置します。  
  
## <a name="wildcards"></a>ワイルドカード  
 .NET Framework 4 では、MSBuild で、Project 属性でのワイルドカードが許可されます。 ワイルドカードがある場合、見つかったすべての一致が並べ替えられ (再現可能性の確保のため)、順序が明示的に設定されていたかのように、その順序でインポートされます。  
  
 これは、機能拡張ポイントを提供して、自身がファイル名をインポート対象のファイルに明示的に追加しなくても、他のユーザーがファイルをインポートできるようにする場合に便利です。 このために、Microsoft.Common.Targets ではファイルの先頭に次の行が含まれています。  
  
```  
<Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore\*" Condition="'$(ImportByWildcardBeforeMicrosoftCommonTargets)' == 'true' and exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\$(MSBuildThisFile)\ImportBefore')"/>  
```  
  
## <a name="example"></a>例  
 次の例は、いくつかの項目やプロパティがあり、一般的なプロジェクト ファイルをインポートするプロジェクトを示しています。  
  
```  
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
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)   
 [方法: 複数のプロジェクト ファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
