---
title: プロジェクト要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 335a1e4efa62f07e10bb24b9971627d24bb13273
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701997"
---
# <a name="project-element-visual-studio-templates"></a>プロジェクト要素
プロジェクトに追加するファイルまたはディレクトリを指定します。

 \<VSTemplate \<> テンプレート\<コンテンツ>プロジェクト>

## <a name="syntax"></a>構文

```
<Project
    File="MyProject.proj"
    TargetFileName="MyTargetProject.proj"
    ReplaceParameters="true/false">
    IgnoreProjectParameter="$myCustomParameter$"
        ...
</Project>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`File`|必須の属性です。<br /><br /> テンプレート *.zip*ファイル内のプロジェクト ファイルの名前を指定します。|
|`ReplaceParameters`|省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに置き換える必要があるパラメーター値をプロジェクト ファイルに含めるかどうかを指定するブール値。 既定値は `false` です。|
|`TargetFileName`|省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときのプロジェクト ファイルの名前を指定します。|
|`IgnoreProjectParameter`|省略可能な属性です。<br /><br /> プロジェクトを現在のソリューションに追加するかどうかを指定します。 カスタム パラメーターの値 "$*myCustomParameter*$" がパラメーター置換ファイルに存在する場合、プロジェクトは作成されますが、現在開いているソリューションの一部としては追加されません。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[フォルダー](../extensibility/folder-element-visual-studio-project-templates.md)|省略可能な要素です。<br /><br /> プロジェクトに追加するフォルダを指定します。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|省略可能な要素です。<br /><br /> プロジェクトに追加するファイルを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必須の要素です。|

## <a name="remarks"></a>Remarks
 `Project` は、`TemplateContent` の子要素で、省略可能な要素です。

 要素`Project`はプロジェクトを指定するために使用されるため、プロジェクト テンプレートでのみ有効です。

 `Project`要素は[、フォルダー](../extensibility/folder-element-visual-studio-project-templates.md)子要素または[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)子要素を持つことができますが、`Folder`両方`ProjectItem`の子要素の混在はできません。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]**[新しい**プロジェクト] ダイアログ ボックスでユーザーが入力した名前に基づいて、プロジェクト ファイル名の名前が自動的に変更されます。 テンプレートで`TargetFileName`作成されたプロジェクト ファイルに代替ファイル名を指定する場合は、 属性を使用します。

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
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [プロジェクト項目要素](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [フォルダー要素 (Visual Studio プロジェクト テンプレート)](../extensibility/folder-element-visual-studio-project-templates.md)
