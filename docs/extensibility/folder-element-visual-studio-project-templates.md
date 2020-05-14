---
title: フォルダー要素 (Visual Studio プロジェクト テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cb256b8be0dd9ce68f193750bf3ff5a383d5f073
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711468"
---
# <a name="folder-element-visual-studio-project-templates"></a>フォルダー要素 (Visual Studio プロジェクト テンプレート)
プロジェクトに追加するフォルダを指定します。

 \<VSTemplate \<> テンプレート\<プロジェクト\<> フォルダー>>コンテンツ

## <a name="syntax"></a>構文

```
<Folder Name="Project Folder">
    <Folder> ... </Folder>
    <ProjectItem> ... </ProjectItem>
</Folder>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須の属性です。<br /><br /> プロジェクト フォルダーの名前。|
|`TargetFolderName`|省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときにフォルダに付ける名前を指定します。 この属性は、パラメーター置換を使用してフォルダー名を作成したり *、.zip*ファイルで直接使用できない国際文字列を持つフォルダーの名前を付けたりするのに便利です。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|`Folder`|プロジェクトに追加するフォルダを指定します。 `Folder`要素には子`Folder`要素を含めることができます。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|プロジェクトに追加するファイルを指定します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|[オプション](../extensibility/templatecontent-element-visual-studio-templates.md)の子要素です。|

## <a name="remarks"></a>Remarks
 `Folder`は オプションの子`Project`です。

 次のいずれかの方法を使用して、プロジェクト項目をテンプレート内のフォルダーに整理できます。

- テンプレート *.zip*ファイルにフォルダーを含め、要素を含めず`Folder`に要素内のファイルへのパスを指定して *、.vstemplate* `ProjectItem`ファイル内のプロジェクトに追加します。 これが推奨される方法です。 次に例を示します。

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレート *.zip*ファイルにフォルダーを含め、要素を含`Folder`む *.vstemplate*ファイル内のプロジェクトに追加します。 次に例を示します。

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- テンプレート *.zip*ファイルにフォルダーを含めるのではなく、要素の属性`TargetFileName`を使用して`ProjectItem`フォルダーを追加します。 次に例を示します。

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>例
 次の例は、Windows アプリケーションのプロジェクト テンプレートのメタデータ[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]を示しています。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <Folder Name="Properties">
                <ProjectItem>AssemblyInfo.cs</ProjectItem>
                <ProjectItem>Resources.resx</ProjectItem>
                <ProjectItem>Resources.Designer.cs</ProjectItem>
                <ProjectItem>Settings.settings</ProjectItem>
                <ProjectItem>Settings.Designer.cs</ProjectItem>
            </Folder>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)
