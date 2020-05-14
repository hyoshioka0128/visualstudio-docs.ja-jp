---
title: テンプレートデータ要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateData
helpviewer_keywords:
- TemplateData element [Visual Studio project templates]
ms.assetid: db17ec9b-bfdf-46b1-bbe7-5ccc140056e2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3ce0226286e8cc4623b66c043eb7bd376597118
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699192"
---
# <a name="templatedata-element-visual-studio-templates"></a>TemplateData 要素 (Visual Studio テンプレート)
テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。

 \<テンプレート>\<データ>

## <a name="syntax"></a>構文

```
<TemplateData>
    <Name> ... </Name>
    <Description> ... </Description>
    <Icon> ... </Icon>
    <ProjectType> ... </ProjectType>
    ...
</TemplateData>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素

| 要素 | 説明 |
| - | - |
| [名前](../extensibility/name-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **[新しいプロジェクト**] ダイアログ ボックスまたは [新しい項目の**追加**] ダイアログ ボックスに表示されるテンプレートの名前を指定します。 |
| [説明](../extensibility/description-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **[新しいプロジェクト**] ダイアログ ボックスまたは [新しい項目の**追加**] ダイアログ ボックスに表示されるテンプレートの説明を指定します。 |
| [アイコン](../extensibility/icon-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> テンプレートの [**新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスに表示されるアイコンとして機能するイメージ ファイルのパスとファイル名を指定します。 |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> [新しいプロジェクト] ダイアログ ボックスで指定したグループの下に表示されるように **、プロジェクト**テンプレートを分類します。 |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [新しいプロジェクト] ダイアログ ボックスで指定したサブカテゴリの下に表示されるように **、プロジェクト**テンプレートを分類します。 |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレート ID を指定します。 |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレート グループ ID を指定します。 |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> **[新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスに表示されるテンプレートの中で、同じカテゴリのテンプレートの中で、テンプレートを整列するために使用する値を指定します。 |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトのインスタンス化時に、含むフォルダーを作成するかどうかを指定します。 |
| [デフォルト名](../extensibility/defaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトまたは項目の作成時に Visual Studio プロジェクト システムが生成する名前を指定します。 |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> Visual Studio プロジェクト システムが作成されるときに、プロジェクトまたは項目の既定の名前を生成するかどうかを指定します。 |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトを一時プロジェクトとして作成できるかどうかを指定します (Visual Studio 2017 のみ)。 |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [**新しいプロジェクト**] ダイアログ ボックスで **[参照**] ボタンを使用できるように設定します。 |
| [[非表示]](../extensibility/hidden-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートを **[新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスに表示するかどうかを指定します。 |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [**新しいプロジェクト**] ダイアログ ボックスにテンプレートを表示する親カテゴリの数を指定します。 |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | 省略可能な要素です。 |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | 省略可能な要素です。<br /><br /> [**新しいプロジェクト**] ダイアログ ボックスの **[場所**] テキスト ボックスを、プロジェクト テンプレートに対して有効、無効、または非表示にするかどうかを指定します。 |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> この要素は、テンプレートが .NET Framework の特定の最小バージョンとそれ以降のバージョン (存在する場合) のみをサポートする場合に使用します。 |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが Web プロジェクトのマスター ページをサポートするかどうかを指定します。 |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが Web プロジェクトのコード分離をサポートするか、分離コード ページ モデルをサポートするかを指定します。 |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが複数の言語で同一かどうか、および [**新しいプロジェクト**] ダイアログ ボックスで **[言語**] オプションを使用できるかどうかを指定します。 |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクト テンプレートの対象となるプラットフォームを指定します。 この要素は、プロジェクト テンプレートを使用してアプリ[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)]を作成することを指定します。 |

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれます。|

## <a name="remarks"></a>Remarks
 `TemplateData`は必須要素です。

 省略可能な要素を含まない場合は、その要素の既定値が使用されます。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
