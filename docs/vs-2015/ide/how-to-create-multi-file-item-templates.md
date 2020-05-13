---
title: '方法 : 複数ファイルの項目テンプレートを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, creating multi-file item templates
- multi-file item templates
- item templates, creating multi-file item templates
ms.assetid: fe3c4257-e383-4c80-b8af-c5c521959c33
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e70039f361ac3410a8ddcccb0f139d8bdcb32ed9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668088"
---
# <a name="how-to-create-multi-file-item-templates"></a>方法 : 複数ファイルの項目テンプレートを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

項目テンプレートには 1 つの項目のみを指定できますが、1 つの項目が複数のファイルから構成されている場合があります。 たとえば、Visual Basic の Windows フォーム項目テンプレートには、次の 3 つのファイルが必要です。

- フォームのコードを含む .vb ファイル。

- フォームのデザイナー情報を含む .designer.vb ファイル。

- フォームの埋め込みリソースを含む .resx ファイル。

  複数ファイルの項目テンプレートでは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で項目が作成されるときに正しいファイル名拡張子が使用されるようにするために、パラメーターが必要です。 **テンプレートのエクスポート** ウィザードを使用して項目テンプレートを作成する場合は、これらのパラメーターが自動的に生成されるので、それ以上編集する必要はありません。 次の手順では、正しいファイル名拡張子を作成するためのパラメーターの使用方法について説明します。

### <a name="to-manually-create-a-multi-file-item-template"></a>複数ファイルの項目テンプレートを手動で作成するには

1. 単一ファイルの項目テンプレートと同じように、項目テンプレートを作成します。 詳細については、「[方法 : 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)」を参照してください。

2. すべての `ProjectItem` 要素に `TargetFileName` 属性を追加します。 `TargetFileName` 属性の値を $fileinputname$.*FileExtension* に設定します。ここで、*FileExtension* はテンプレートに含まれるファイルのファイル名拡張子です。 (例:

    ```
    <ProjectItem TargetFileName="$fileinputname$.vb">
        Form1.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
        Form1.Designer.vb
    </ProjectItem>
    <ProjectItem TargetFileName="$fileinputname$.resx">
        Form1.resx
    </ProjectItem>
    ```

     このテンプレートから派生した項目がプロジェクトに追加されると、ユーザーが **[新しい項目の追加]** ダイアログ ボックスに入力した名前に基づいてファイル名が決定されます。

3. テンプレートに含めるファイルを選択して右クリックし、 **[送る]** をクリックしてから **[圧縮 (zip 形式) フォルダー]** をクリックします。 選択したファイルは .zip ファイルに圧縮されます。

4. ユーザー項目テンプレートの場所に .zip ファイルを配置します。 既定では、ディレクトリは \My Documents\Visual Studio *Version*\Templates\ItemTemplates\\ となります。 詳細については、「[方法 : プロジェクト テンプレートと項目テンプレートを配置して整理する](../ide/how-to-locate-and-organize-project-and-item-templates.md)」を参照してください。

## <a name="example"></a>例
 次の例では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Windows フォーム テンプレートを示します。 このテンプレートに基づいて項目が作成された場合、作成された 3 つのファイルの名前は **[新しい項目の追加]** ダイアログ ボックスに入力された名前と一致します。

```
<VSTemplate Version="2.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-file Item Template</Name>
        <Icon>Icon.ico</Icon>
        <Description>An example of a multi-file item template</Description>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectItem TargetFileName="$fileinputname$.vb" SubType="Form">
            Form1.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.Designer.vb">
            Form1.Designer.vb
        </ProjectItem>
        <ProjectItem TargetFileName="$fileinputname$.resx">
            Form1.resx
        </ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>参照
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)[方法: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)[テンプレートパラメーター](../ide/template-parameters.md) [方法: テンプレート内のパラメーターを置き換える](../ide/how-to-substitute-parameters-in-a-template.md)
