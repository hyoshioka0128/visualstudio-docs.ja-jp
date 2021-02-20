---
title: 複数ファイルの項目テンプレートを作成する
description: Visual Studio で複数のファイルから構成される項目テンプレートを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/02/2018
ms.topic: how-to
helpviewer_keywords:
- Visual Studio templates, creating multi-file item templates
- multi-file item templates
- item templates, creating multi-file item templates
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: b375cf54dfe35928a35f991190c94b3d08685827
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875381"
---
# <a name="how-to-create-multi-file-item-templates"></a>方法: 複数ファイルの項目テンプレートを作成する

項目テンプレートには 1 つの項目のみを指定できますが、1 つの項目が複数のファイルから構成されている場合があります。 たとえば、Windows フォーム項目テンプレートには、次の 3 つのファイルが必要です。

- フォームのコードを含むファイル

- フォームのデザイナー情報を含むファイル

- フォームの埋め込みリソースを含むファイル

複数ファイルの項目テンプレートでは、項目が作成されるときに正しいファイル拡張子が使われるようにするため、パラメーターが必要です。 **テンプレートのエクスポート ウィザード** を使って複数ファイルの項目テンプレートを作成する場合、これらのパラメーターは自動的に生成されるので、それ以上編集する必要はありません。

## <a name="use-the-export-template-wizard"></a>[テンプレートのエクスポート] ウィザードを使用する

複数ファイルの項目テンプレートは、単一ファイルの項目テンプレートと同じ方法で作成できます。 「[方法:項目テンプレートを作成する](../ide/how-to-create-item-templates.md)」を参照してください。 ウィザードの **[エクスポートする項目の選択]** ページで、依存ファイル (Windows フォームのフォーム ファイルなど) を持つファイルを選択します。 依存ファイル (デザイナー ファイルやリソース ファイルなど) が、ウィザードによってテンプレートに自動的に追加されます。

## <a name="manually-create-a-multi-file-item-template"></a>複数ファイルの項目テンプレートを手動で作成する

1. 手動で単一ファイルの項目テンプレートを作成するのと同じように項目テンプレートを作成しますが、複数ファイルの項目を構成する各ファイルを組み込みます。

1. *.vstemplate* XML ファイルで、各個別ファイルに対する `ProjectItem` 要素を追加し、この要素に `TargetFileName` 属性を追加します。 `TargetFileName` 属性の値を *$fileinputname$.FileExtension* に設定します。ここで、*FileExtension* はテンプレートに含まれるファイルのファイル拡張子です。 次に例を示します。

    ```xml
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

     > [!NOTE]
     > このテンプレートから派生した項目がプロジェクトに追加されると、ユーザーが **[新しい項目の追加]** ダイアログ ボックスで入力した名前からファイル名が派生されます。

1. テンプレートに組み込むファイルを選んで右クリックし、 **[送る]**  >  **[圧縮 (zip 形式) フォルダー]** の順に選択します。

   選択したファイルは *.zip* ファイルに圧縮されます。

1. ユーザー項目テンプレートの場所に *.zip* ファイルをコピーします。 既定では、このディレクトリは *%USERPROFILE%\Documents\Visual Studio \<Version\>\Templates\ItemTemplates* です。 詳細については、「[方法:テンプレートを配置して整理する](../ide/how-to-locate-and-organize-project-and-item-templates.md)」を参照してください。

1. Visual Studio をいったん閉じて開きなおします。

1. 新しいプロジェクトを作成するか、既存のプロジェクトを開き、 **[プロジェクト]**  >  **[新しい項目の追加]** の順に選ぶか、**Ctrl**+**Shift**+**A** キーを押します。

   複数ファイルの項目テンプレートが、 **[新しい項目の追加]** ダイアログ ボックスに表示されます。

## <a name="example"></a>例

次の例では、Windows フォーム テンプレートを示します。 このテンプレートに基づいて項目が作成された場合、作成された 3 つのファイルの名前は **[新しい項目の追加]** ダイアログ ボックスに入力された名前と一致します。

```xml
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

## <a name="see-also"></a>関連項目

- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [方法: 項目テンプレートを作成する](../ide/how-to-create-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)
- [方法: テンプレート内のパラメーターを置き換える](../ide/how-to-substitute-parameters-in-a-template.md)
