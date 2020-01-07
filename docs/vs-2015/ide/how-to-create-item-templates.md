---
title: '方法 : 項目テンプレートを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project item templates, XML reference
- project item templates, custom template locations
- project item templates, creating
- project item templates, metadata files
ms.assetid: 77bc53d4-d607-4820-a032-7e3b365891b5
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c9edc79002a4a2d7c2fe135d7eb4669f5f010599
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668073"
---
# <a name="how-to-create-item-templates"></a>方法 : 項目テンプレートを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの[最初の手順](#to-add-a-custom-project-item-template-to-the-add-new-item-dialog-box)では、**テンプレートのエクスポート** ウィザードを使って項目テンプレートを作成する方法を示します。 テンプレートを複数のファイルで構成する場合は、「[方法 : 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md)」をご覧ください。

 ウィザードはさまざまな作業を実行して基本テンプレートを作成しますが、多くの場合、テンプレートをエクスポートした後で .vstemplate ファイルを手動で変更する必要があります。 たとえば、[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリ プロジェクトの **[新しい項目の追加]** ダイアログに項目を表示する場合、追加の手順をいくつか実行する必要があります。 このトピックの [2 つ目の手順](#to-enable-the-item-template-to-be-used-in-a-store-project)では、このタスクの実行方法を説明します。

 場合によっては、項目テンプレートをゼロから手動で作成する必要があります。 [3 つ目の手順](#to-enable-templates-for-specific-project-sub-types)では、この方法について説明します。

 .vstemplate ファイルで使用できる要素の詳細については、「[Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」をご覧ください。

### <a name="to-add-a-custom-project-item-template-to-the-add-new-item-dialog-box"></a>カスタム プロジェクト項目テンプレートを [新しい項目の追加] ダイアログ ボックスに追加するには

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] でプロジェクトを作成または開きます。

2. 項目をプロジェクトに追加し、必要に応じて変更します。

3. コード ファイルを変更して、パラメーター置換を行う場所を示します。 詳しくは、「[方法 : テンプレート内のパラメーターを置き換える](../ide/how-to-substitute-parameters-in-a-template.md)」をご覧ください。

4. **[ファイル]** メニューの **[テンプレートのエクスポート]** をクリックします。

5. **[項目テンプレート]** をクリックし、項目を含むプロジェクトを選んで、 **[次へ]** をクリックします。

6. テンプレートを作成する項目を選び、 **[次へ]** をクリックします。

7. テンプレートに含めるアセンブリ参照を選び、 **[次へ]** をクリックします。

8. アイコン ファイル名、プレビュー イメージ、テンプレート名、およびテンプレートの説明を入力し、 **[完了]** をクリックします。

     テンプレートのファイルは .zip ファイルに追加され、ダイアログで指定した任意のディレクトリにコピーされます。 規定の場所は、 **..\Users\\<ユーザー名\>\Documents\Visual Studio \<バージョン>\My Exported Templates\\** フォルダーです。

    > [!WARNING]
    > 旧バージョンの Visual Studio での規定の場所は、 **..\Users\\<ユーザー名\>\Documents\Visual Studio \<バージョン>\Templates\ItemTemplates** です。

### <a name="to-enable-the-item-template-to-be-used-in-a-store-project"></a>ストア プロジェクトで項目テンプレートを使用できるようにするには

1. 上記の手順に従って、項目テンプレートをエクスポートします。

2. ..\Users\\*ユーザー名*\Documents\Visual Studio *バージョン*\Templates\ItemTemplates\ (または **My Exported Templates**) フォルダーにコピーされた .zip ファイルから、.vstemplate ファイルを抽出します。

3. Visual Studio で .vstemplate ファイルを開きます。

4. Windows 8.1 ストア用の C# プロジェクトの場合は、.vstemplate ファイルで `<TemplateData>` の開始タグと終了タグの中に XML、`<TemplateGroupID>WinRT-Managed</TemplateGroupID>` を追加します。

    Windows 8.1 ストア用の C++ プロジェクトでは、値として `WinRT-Native-6.3` を使用します。 Windows 10 およびその他の種類のプロジェクトの場合については、「[TemplateGroupID 要素 (Visual Studio テンプレート)](../extensibility/templategroupid-element-visual-studio-templates.md)」をご覧ください。

    次の例は、XML 行 `<TemplateGroupID>WinRT-Managed</TemplateGroupID>` が追加された後の .vstemplate ファイルの内容全体を示しています。 この例は、C# プロジェクトに固有です。 @No__t_0ProjectType > と \< [Templategroupid](../extensibility/templategroupid-element-visual-studio-templates.md)> 要素を変更して、他の言語およびプロジェクトの種類を指定することができます。

   ```xml
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
     <TemplateData>
       <DefaultName>MyItemStoreTemplate.xaml</DefaultName>
       <Name>MyItemStoreTemplate</Name>
       <Description>This is an example itemtemplate</Description>
       <ProjectType>CSharp</ProjectType>
       <SortOrder>10</SortOrder>
       <Icon>__TemplateIcon.ico</Icon>
       <TemplateGroupID>WinRT-Managed</TemplateGroupID>
     </TemplateData>
     <TemplateContent>
       <References />
       <ProjectItem SubType="Designer" TargetFileName="$fileinputname$.xaml" ReplaceParameters="true">MyItemTemplate.xaml</ProjectItem>
       <ProjectItem SubType="Code" TargetFileName="$fileinputname$.xaml.cs" ReplaceParameters="true">MyItemTemplate.xaml.cs</ProjectItem>
     </TemplateContent>
   </VSTemplate>
   ```

    他に使用可能な TemplateGroupID の値については、「[TemplateGroupID 要素 (Visual Studio テンプレート)](../extensibility/templategroupid-element-visual-studio-templates.md)」をご覧ください。 .vstemplate の総合的なリファレンスについては、「[Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」をご覧ください。

5. Visual Studio で、.vstemplate ファイルを保存して閉じます。

6. .vstemplate ファイルをコピーし、..\Users\\*ユーザー名*\Documents\Visual Studio *バージョン*\Templates\ItemTemplates\ フォルダーにある .zip ファイルに貼り付けます。

    **[ファイルのコピー]** ダイアログ ボックスが表示されたら、 **[コピーして置き換える]** をクリックします。

   これで、 **[新しい項目の追加]** ダイアログ ボックスを使って、このテンプレートに基づく項目を [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] プロジェクトに追加できます。

   パラメーター名の詳細については、「[テンプレート パラメーター](../ide/template-parameters.md)」をご覧ください。

### <a name="to-enable-templates-for-specific-project-sub-types"></a>特定のプロジェクト サブタイプ用のテンプレートを有効にするには

1. 開発環境では、特定のプロジェクトに対して、[項目の追加] ダイアログ ボックスからプロジェクト項目を使用可能にすることができます。 この手順を使用して、Windows プロジェクト、Web プロジェクト、Office プロジェクト、データベース プロジェクトでカスタム項目を使用可能にすることができます。

    項目テンプレートの .vstemplate ファイルで、ProjectType 要素を探します。

    [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) 要素を ProjectType 要素の直後に追加します。

2. 要素のテキスト値を次のいずれかの値に設定します。

   1. Windows

   2. Office

   3. データベース

   4. Web

      たとえば、`<ProjectSubType>Database</ProjectSubType>` のように指定します。

      Office プロジェクトで使用可能な項目テンプレートの例を次に示します。

   ```
   <VSTemplate Version="2.0.0" Type="Item" Version="2.0.0">
       <TemplateData>
           <Name>Class</Name>
           <Description>An empty class file</Description>
           <Icon>Class.ico</Icon>
           <ProjectType>CSharp</ProjectType>
           <ProjectSubType>Office</ProjectSubType>
           <DefaultName>Class.cs</DefaultName>
       </TemplateData>
       <TemplateContent>
           <ProjectItem>Class1.cs</ProjectItem>
       </TemplateContent>
   </VSTemplate>

   ```

### <a name="to-manually-create-an-item-template-without-using-the-export-template-wizard"></a>テンプレートのエクスポート ウィザードを使用せずに項目テンプレートを手動で作成するには

1. プロジェクトとプロジェクト項目を作成します。

2. プロジェクト項目を変更して、テンプレートとして保存できる状態にします。

3. 必要に応じて、コード ファイルを変更し、パラメーター置換を行う場所を示します。 パラメーター置換の詳細については、「方法 : テンプレート内のパラメーターを置き換える」を参照してください。

4. XML ファイルを作成し、.vstemplate のファイル名拡張子を使用して、新しい項目テンプレートと同じディレクトリに保存します。

5. 項目テンプレート メタデータを提供するための .vstemplate XML ファイルを作成します。 詳しくは、「[Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」と前のセクションの例をご覧ください。

6. .vstemplate ファイルを保存して閉じます。

7. エクスプローラーで、テンプレートに含めるファイルを選択します。右クリックして [送信] をクリックし、[圧縮 (zip 形式) フォルダー] をクリックします。 選択したファイルは .zip ファイルに圧縮されます。

8. .zip ファイルをコピーして、ユーザーの項目テンプレートの場所に貼り付けます。 Visual Studio 2015 での既定のディレクトリは、..\Users\\<ユーザー名\>\Documents\Visual Studio 2015\Templates\ItemTemplates\\ です。 詳細については、「方法 : プロジェクト テンプレートと項目テンプレートを配置して整理する」を参照してください。

## <a name="see-also"></a>参照
 [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)[方法: 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md) [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
