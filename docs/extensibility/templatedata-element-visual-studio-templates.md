---
title: TemplateData 要素 (Visual Studio テンプレート) |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699192"
---
# <a name="templatedata-element-visual-studio-templates"></a>TemplateData 要素 (Visual Studio テンプレート)
テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。

 \<VSTemplate> \<TemplateData>

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
 なし。

### <a name="child-elements"></a>子要素

| 要素 | 説明 |
| - | - |
| [名前](../extensibility/name-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **新しいプロジェクト**または [**新しい項目の追加**] ダイアログボックスに表示されるテンプレートの名前を指定します。 |
| [説明](../extensibility/description-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> **新しいプロジェクト**または [**新しい項目の追加**] ダイアログボックスに表示されるテンプレートの説明を指定します。 |
| [Icon](../extensibility/icon-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> アイコンとして機能するイメージファイルのパスとファイル名を指定します。このアイコンは、 **新しいプロジェクト** または [ **新しい項目の追加** ] ダイアログボックスで、テンプレートに対して表示されます。 |
| [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) | 必須の要素です。<br /><br /> [ **新しいプロジェクト** ] ダイアログボックスの指定したグループの下に表示されるように、プロジェクトテンプレートを分類します。 |
| [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトテンプレートを分類して、[ **新しいプロジェクト** ] ダイアログボックスの指定したサブカテゴリの下に表示されるようにします。 |
| [TemplateID](../extensibility/templateid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレート ID を指定します。 |
| [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートグループ ID を指定します。 |
| [SortOrder](../extensibility/sortorder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスに表示されるテンプレートを、同じカテゴリの他のテンプレートの中に配置するために使用される値を指定します。 |
| [CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトのインスタンス化で、格納フォルダーを作成するかどうかを指定します。 |
| [Defaultname,](../extensibility/defaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトまたはアイテムの作成時に Visual Studio プロジェクトシステムによって生成される名前を指定します。 |
| [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトまたは項目の作成時に、Visual Studio プロジェクトシステムで既定の名前を生成するかどうかを指定します。 |
| [PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクトを一時プロジェクトとして作成できるかどうかを指定します (Visual Studio 2017 のみ)。 |
| [EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [**新しいプロジェクト**] ダイアログボックスで [**参照**] ボタンを使用できるようにするかどうかを指定します。これにより、新しいプロジェクトを保存する既定のディレクトリをユーザーが簡単に変更できるようになります。 |
| [[非表示]](../extensibility/hidden-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスのいずれかにテンプレートを表示するかどうかを指定します。 |
| [NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> [ **新しいプロジェクト** ] ダイアログボックスにテンプレートを表示する親カテゴリの数を指定します。 |
| [LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md) | 省略可能な要素です。 |
| [LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md) | 省略可能な要素です。<br /><br /> [**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスが、プロジェクトテンプレートに対して [有効]、[無効]、または [非表示] のどちらであるかを指定します。 |
| [RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが、.NET Framework の特定の最小バージョン、およびそれ以降のバージョンをサポートしている場合にのみ、この要素を使用します。 |
| [SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが web プロジェクトのマスターページをサポートするかどうかを指定します。 |
| [SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが web プロジェクトのコード分離または分離コードページモデルをサポートするかどうかを指定します。 |
| [SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> テンプレートが複数の言語に対して同一であるかどうか、および [**新しいプロジェクト**] ダイアログボックスから**言語**オプションを使用できるかどうかを指定します。 |
| [TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md) | 省略可能な要素です。<br /><br /> プロジェクト テンプレートの対象となるプラットフォームを指定します。 この要素は、アプリを作成するためにプロジェクトテンプレートを使用することを指定し [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] ます。 |

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクトテンプレート、項目テンプレート、またはスタートキットのすべてのメタデータが含まれます。|

## <a name="remarks"></a>解説
 `TemplateData` は必須の要素です。

 省略可能な要素を含めない場合は、その要素の既定値が使用されます。

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
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
