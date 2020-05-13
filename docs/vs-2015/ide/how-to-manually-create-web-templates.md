---
title: '方法 : Web テンプレートを手動で作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, Web
- templates [Visual Studio], Web
- Web templates [Visual Studio]
- project templates [Visual Studio], Web
ms.assetid: 731c4027-a152-48c5-bfc4-93490bf1949f
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4bf604e747158c651f284c6463c2c2f65ae3c47a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651800"
---
# <a name="how-to-manually-create-web-templates"></a>方法 : Web テンプレートを手動で作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Web テンプレートの作成方法は、他の種類のテンプレートを作成する場合と異なります。 Web プロジェクト テンプレートは **[新しい Web サイトの追加]** ダイアログ ボックスに表示され、Web プロジェクトの項目はプログラミング言語によって分類されるので、.vstemplate ファイルではテンプレートを Web テンプレートとして指定し、プログラミング言語を示す必要があります。

> [!NOTE]
> Web テンプレートには、`Project` 要素の `File` 属性を使って指定される空の .webproj ファイルが含まれる必要があります。 Web プロジェクトではプロジェクト ファイルは必要ありませんが、Web テンプレートが正しく機能するためにはこのファイルが必要です。

### <a name="to-manually-create-a-web-template"></a>Web テンプレートを手動で作成するには

1. Web プロジェクトを作成します。

2. プロジェクト内のファイルを変更または削除するか、新しいファイルをプロジェクトに追加します。

3. XML ファイルを作成し、.vstemplate ファイル名拡張子を使って、プロジェクトと同じディレクトリに保存します。 このファイルを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のプロジェクトに追加しないでください。

4. プロジェクト テンプレート メタデータを提供するための .vstemplate XML ファイルを作成します。 詳しくは、次のセクションの例をご覧ください。

5. .vstemplate ファイルで `ProjectType` 要素を探し、テキスト値を `Web` に設定します。

6. `ProjectType` 要素の後に `ProjectSubType` 要素を追加し、テキスト値をテンプレートのプログラミング言語に設定します。 プログラミング言語は次のいずれかの値です。

   - CSharp

   - VisualBasic

     (例:

   ```
   <TemplateData>
       ...
       <ProjectType>Web</ProjectType>
       <ProjectSubType>CSharp</ProjectSubType>
       ...
   </TemplateData>
   ```

7. テンプレート内のファイル (.vstemplate ファイルを含む) を選んで右クリックし、 **[送信]** をクリックして、 **[圧縮 (zip 形式) フォルダー]** をクリックします。 ファイルは .zip ファイルに圧縮されます。

8. .zip テンプレート ファイルを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト テンプレートのディレクトリに配置します。 既定では、このディレクトリは \My Documents\Visual Studio <*バージョン*>\My Exported Templates\\ です。

## <a name="example"></a>例
 次の例では、Web プロジェクト テンプレートの基本的な .vstemplate ファイルを示します。

```
<VSTemplate Version="2.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>参照
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md) [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
