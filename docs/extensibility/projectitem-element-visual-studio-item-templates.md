---
title: プロジェクトアイテム要素 (Visual Studio 項目テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6826440ed12e90f1ffced63dfef45bb3d86177ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701875"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>ProjectItem 要素 (Visual Studio 項目テンプレート)
項目テンプレートに含まれるファイルを指定します。

> [!NOTE]
> 要素`ProjectItem`は、テンプレートがプロジェクトまたは項目のどちらに対して使用されているかに応じて、異なる属性を受け入れます。 このトピックでは、`ProjectItem`項目の要素について説明します。 プロジェクト テンプレートの要素`ProjectItem`の説明については、「プロジェクト[アイテム要素 (Visual Studio プロジェクト テンプレート)」](../extensibility/projectitem-element-visual-studio-project-templates.md)を参照してください。

 \<VSTemplate \<> テンプレート\<プロジェクト アイテム>>コンテンツ

## <a name="syntax"></a>構文

```
<ProjectItem
    SubType="Form/Component/CustomControl/UserControl"
    CustomTool="string"
    ItemType="string"
    ReplaceParameters="true/false"
    TargetFileName="TargetFileName.ext">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|---------------------| - |
| `SubType` | 省略可能な属性です。<br /><br /> 複数ファイルの項目テンプレート内の項目のサブタイプを指定します。 この値は、アイテムを開くために使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]するエディターを決定するために使用されます。 |
| `CustomTool` | 省略可能な属性です。<br /><br /> プロジェクト ファイル内の項目のカスタム ツールを設定します。 |
| `ItemType` | 省略可能な属性です。<br /><br /> プロジェクト ファイル内の項目の ItemType を設定します。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> テンプレートからプロジェクトを作成するときに置き換える必要があるパラメーター値を項目に含めるかどうかを指定するブール値。 既定値は `false` です。 |
| `TargetFileName` | 省略可能な属性です。<br /><br /> テンプレートから作成される項目の名前を指定します。 この属性は、パラメーター置換を使用して項目名を作成する場合に便利です。 |

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テンプレート`string` *.zip*ファイル内のファイルの名前を表す A。

## <a name="remarks"></a>Remarks
 `ProjectItem`は オプションの子`TemplateContent`です。

 この`TargetFileName`属性を使用して、ファイルの名前をパラメーターに変更できます。 たとえば *、MyFile.vb*ファイルがテンプレート *.zip*ファイルのルート ディレクトリに存在するが、**新しい項目の追加**] ダイアログ ボックスでユーザーが指定したファイル名に基づいてファイル名を付ける場合は、次の XML を使用します。

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 このテンプレートからアイテムを作成する場合、ファイル名はユーザーが **[新しい項目の追加**] ダイアログ ボックスに入力した名前に基づいて作成されます。 これは、複数ファイルの項目テンプレートを作成する場合に便利です。 詳細については、「[方法 : 複数ファイルの項目テンプレートを作成](../ide/how-to-create-multi-file-item-templates.md)する」および「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

## <a name="example"></a>例
 クラスの標準項目テンプレートのメタデータを次の例に[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]示します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法 : 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
