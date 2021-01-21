---
title: Visual Studio での SharePoint ツールの拡張機能の配置 |Microsoft Docs
description: Visual Studio の SharePoint ツールの拡張機能を配置します。 VSIX パッケージを作成するには、Visual Studio 拡張機能 (VSIX) プロジェクトを使用します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9c8b05b5cb74a28157436f95f01992515c716e6a
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672679"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Visual Studio での SharePoint ツールの拡張機能の配置

SharePoint ツールの拡張機能を配置するには、拡張機能 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイルを含む拡張機能 (VSIX) パッケージを作成します。 VSIX パッケージは、Open パッケージング規約 (OPC) 標準に従い、圧縮されたファイルです。 VSIX パッケージには、 *.vsix* という拡張子が付いています。

VSIX パッケージを作成した後、他のユーザーは .vsix ファイルを実行して拡張機能をインストールできます。 ユーザーが拡張機能をインストールすると、すべてのファイルが%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions フォルダーにインストールされます。 拡張機能をデプロイするには、VSIX パッケージを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードするか、ネットワーク共有や他の web サイトでパッケージをホストするなど、他の方法で顧客にパッケージを配布することができます。

VSIX パッケージの作成と [Visual Studio Marketplace](https://marketplace.visualstudio.com/)への配置の詳細については、「 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 Vsix パッケージを作成するには、Visual Studio で **Vsix プロジェクト** テンプレートを使用するか、vsix パッケージを手動で作成します。

## <a name="use-vsix-projects-to-create-vsix-packages"></a>Vsix プロジェクトを使用した VSIX パッケージの作成

Visual Studio SDK に用意されている **Vsix プロジェクト** テンプレートを使用して、SharePoint ツールの拡張機能の vsix パッケージを作成できます。 Vsix プロジェクトを使用すると、手動で VSIX パッケージを作成するよりも多くのメリットが得られます。

- プロジェクトをビルドすると、Visual Studio によって VSIX パッケージが自動的に生成されます。 パッケージに配置ファイルを追加し、パッケージの [Content_Types] .xml ファイルを作成するなどのタスクが実行されます。

- Vsix プロジェクトを構成して、拡張機能プロジェクトのビルド出力と、プロジェクトテンプレートや項目テンプレートなどの他のファイルを VSIX パッケージに含めることができます。

VSIX プロジェクトの使用方法の詳細については、「 [Vsix プロジェクトテンプレート](../extensibility/vsix-project-template.md)」を参照してください。

### <a name="organize-your-projects"></a>プロジェクトを整理する

既定では、VSIX プロジェクトは、アセンブリではなく、VSIX パッケージのみを生成します。 そのため、通常は、VSIX プロジェクトに SharePoint ツールの拡張機能を実装しません。 一般に、少なくとも2つのプロジェクトを使用します。

- VSIX プロジェクト。

- 拡張機能を実装するクラスライブラリプロジェクト。

また、特定の種類の拡張機能の追加プロジェクトを使用することもできます。

- 拡張機能によって使用される任意の SharePoint コマンドを実装するクラスライブラリプロジェクト。 このシナリオを示すチュートリアルについては、「 [チュートリアル: web パーツを表示するためのサーバーエクスプローラーの拡張](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

- 項目テンプレートまたはプロジェクトテンプレートプロジェクト。拡張機能で SharePoint プロジェクト項目の新しい種類が定義されている場合は、項目テンプレートまたはプロジェクトテンプレートを作成します。 このシナリオを示すチュートリアルについては、「 [チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」を参照してください。

- 拡張機能にテンプレートが含まれている場合に、項目テンプレートまたはプロジェクトテンプレートのカスタムウィザードを実装するクラスライブラリプロジェクト。 このシナリオを示すチュートリアルについては、「 [チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)」を参照してください。

すべてのプロジェクトを同じ Visual Studio ソリューションに含める場合は、VSIX プロジェクトの source.extension.vsixmanifest ファイルを変更して、クラスライブラリプロジェクトのビルド出力を含めることができます。

### <a name="edit-the-vsix-manifest"></a>VSIX マニフェストを編集する

拡張機能に含めるすべての項目のエントリを含めるには、VSIX プロジェクトの source.extension.vsixmanifest ファイルを編集する必要があります。 ショートカットメニューから source.extension.vsixmanifest ファイルを開くと、ファイルがデザイナーに表示されます。このファイルには、ファイル内の XML を編集するための UI が用意されています。 詳細については、「 [VSIX マニフェストデザイナー](../extensibility/vsix-manifest-designer.md)」を参照してください。

次の項目について、source.extension.vsixmanifest ファイルにエントリを追加する必要があります。

- 拡張アセンブリ。

- 拡張機能によって使用される任意の SharePoint コマンドを実装するアセンブリ。

- 拡張機能に関連付けられているプロジェクトテンプレートまたは項目テンプレート。

- 拡張機能に関連付けられているテンプレートのカスタムウィザード。

次の手順では、これらの各項目の source.extension.vsixmanifest ファイルにエントリを追加する方法について説明します。

#### <a name="to-include-the-extension-assembly"></a>拡張機能アセンブリを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[ **開く**] を選択します。

     デザイナーでファイルが開きます。

2. エディターの [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

3. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

4. [ **ソース** ] ボックスの一覧で、次のいずれかの手順を実行します。

    - 拡張機能アセンブリが、VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされている場合は、 **現在のソリューション内のプロジェクト** を選択します。 [ **プロジェクト** ] ボックスの一覧で、プロジェクトの名前を選択します。

    - 拡張機能アセンブリがファイルとしてプロジェクトに含まれている場合は、[ **ファイルシステム上のファイル**] を選択します。 [ **パス** ] の一覧で、拡張機能アセンブリファイルの完全なパスを入力するか、[ **参照** ] ボタンを使用してアセンブリファイルを検索して選択します。

5. **[OK]** を選択します。

#### <a name="to-include-a-sharepoint-command-assembly"></a>SharePoint コマンドアセンブリを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[ **開く** ] をクリックします。

     デザイナーでファイルが開きます。

2. エディターの [ **アセット** ] セクションで、[ **新規** ] ボタンを選択します。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

3. [ **種類** ] ボックスに「 **SharePoint. コマンド. v4**」と入力します。

4. [ **ソース** ] ボックスの一覧で、次のいずれかの手順を実行します。

    - コマンドアセンブリが VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされている場合は、 **現在のソリューション内のプロジェクト** を選択します。 [ **プロジェクト** ] ボックスの一覧で、プロジェクトの名前を選択します。

    - コマンドアセンブリがプロジェクト内のファイルとして含まれている場合は、[ **ファイルシステム上のファイル**] を選択します。 [ **パス** ] の一覧で、拡張機能アセンブリファイルの完全なパスを入力するか、[ **参照** ] ボタンを使用してアセンブリファイルを検索して選択します。

5. **[OK]** を選択します。

#### <a name="to-include-a-template-that-you-create"></a>作成するテンプレートを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[ **開く** ] をクリックします。

     デザイナーでファイルが開きます。

2. エディターの [ **アセット** ] セクションで、[ **新規** ] ボタンを選択します。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

3. [ **種類** ] ボックスの一覧で、 **VisualStudio** または **VisualStudio** を選択します。

4. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** を選択します。

5. [ **プロジェクト** ] ボックスの一覧で、プロジェクトの名前を選択し、[ **OK** ] をクリックします。

6. **ソリューションエクスプローラー** で、プロジェクトテンプレートまたは項目テンプレートプロジェクトのショートカットメニューを開き、[**プロジェクトのアンロード**] をクリックします。

7. プロジェクトノードのショートカットメニューをもう一度開き、[_テンプレート_ の **編集**] を選択するか、_テンプレート projectname_**. .vbproj** を **編集****します。**

8. プロジェクト ファイルで次の `VSTemplate` 要素を見つけます。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. この要素を次の XML に置き換えます。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath` 要素は、プロジェクトをビルドするとプロジェクト テンプレートが作成されるパス内の追加フォルダーを指定します。 ここで指定するフォルダーでは、顧客が [ **新しいプロジェクトの追加** ] ダイアログボックスを開いたときにのみ項目テンプレートを使用できるようにし、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

10. ファイルを保存して閉じます。

11. **ソリューションエクスプローラー** で、プロジェクトテンプレートまたは項目テンプレートプロジェクトのショートカットメニューを開き、[**プロジェクトの再読み込み**] をクリックします。

#### <a name="to-include-a-template-that-you-create-manually"></a>手動で作成したテンプレートを含めるには

1. VSIX プロジェクトで、テンプレートを格納する新しいフォルダーをプロジェクトに追加します。

2. この新しいフォルダーの下に次のサブフォルダーを作成し、テンプレート (.zip) ファイルを *ロケール ID* フォルダーに追加します。

     *自分のテンプレートフォルダー*

     **SharePoint**

     **SharePoint14**

     *ロケール ID*

     自分の *templatename*.zip

     たとえば、英語 (米国) のロケールをサポートする ContosoCustomAction.zip という名前の項目テンプレートがある場合、完全なパスは *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip* 可能性があります。

3. **ソリューションエクスプローラー** で、テンプレートファイル (ファイル名) を選択 *します。*

4. [ **プロパティ** ] ウィンドウで、[ **ビルドアクション** ] プロパティを [ **コンテンツ**] に設定します。

5. Source.extension.vsixmanifest ファイルのショートカットメニューを開き、[ **開く**] を選択します。

     デザイナーでファイルが開きます。

6. エディターの [ **アセット** ] セクションで、[ **新規** ] ボタンを選択します。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

7. [ **種類** ] ボックスの一覧で、 **VisualStudio** または **VisualStudio** を選択します。

8. [ **ソース** ] ボックスの一覧で、[ **ファイルシステム上のファイル**] を選択します。

9. [ **パス** ] フィールドに、アセンブリへの完全なパス (たとえば、 *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*) を入力するか、[ **参照** ] ボタンを使用してアセンブリを検索して選択し、[ **OK** ] をクリックします。

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>プロジェクトテンプレートまたは項目テンプレートにウィザードを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[ **開く**] を選択します。

     デザイナーでファイルが開きます。

2. エディターの [ **アセット** ] セクションで、[ **新規** ] ボタンを選択します。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

3. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

4. [ **ソース** ] ボックスの一覧で、次のいずれかの手順を実行します。

    - ウィザードアセンブリが VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされている場合は、 **現在のソリューション内のプロジェクト** を選択します。 [ **プロジェクト** ] ボックスの一覧で、プロジェクトの名前を選択します。

    - ウィザードアセンブリがプロジェクト内のファイルとして含まれている場合は、[ **ファイルシステム上のファイル**] を選択します。 [ **パス** ] フィールドにアセンブリファイルへの完全なパスを入力するか、[ **参照** ] ボタンを使用してアセンブリを探して選択します。

5. **[OK]** を選択します。

### <a name="related-walkthroughs"></a>関連するチュートリアル

次の表に、VSIX プロジェクトを使用してさまざまな種類の SharePoint ツール拡張機能を配置する方法を示すチュートリアルを示します。

|拡張機能の種類|関連するチュートリアル|
|--------------------|--------------------------|
|拡張機能アセンブリのみを含む拡張機能|[チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [チュートリアル: SharePoint プロジェクト拡張機能の作成](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [チュートリアル: サーバーエクスプローラーの拡張機能で SharePoint クライアントオブジェクトモデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|SharePoint コマンドを含む拡張機能|[チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|Visual Studio テンプレートを含む拡張機能|[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|テンプレートウィザードを含む拡張機能|[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>VSIX パッケージを手動で作成する

SharePoint ツール拡張機能の VSIX パッケージを手動で作成する場合は、次の手順を実行します。

1. 新しいフォルダーに source.extension.vsixmanifest ファイルと [Content_Types] .xml ファイルを作成します。 詳細については、「 [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

2. Windows エクスプローラーで、2つの XML ファイルが含まれているフォルダーを右クリックし、[送信] をクリックして、[圧縮 (zip 形式) フォルダー] をクリックします。 結果として得られる .zip ファイルの名前を Filename.vsix に変更します。ここで Filename には、パッケージをインストールする再頒布可能なファイルの名前を指定します。

3. 拡張機能アセンブリを VSIX パッケージに追加します。 拡張機能に SharePoint コマンドが含まれている場合は、SharePoint コマンドを実装するアセンブリを VSIX パッケージに追加することもできます。

4. Source.extension.vsixmanifest ファイルを変更します。

    - 要素の `Microsoft.VisualStudio.MefComponent` 下に要素を追加 `Assets` し、新しい要素の値を、VSIX パッケージ内の拡張機能を実装するアセンブリの相対パスに設定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

    - SharePoint のサーバーオブジェクトモデルを呼び出す SharePoint コマンドが拡張機能に含まれている場合は、要素の下に要素を追加し `Microsoft.VisualStudio.Assembly` `Assets` ます。 新しい要素の値を、VSIX パッケージ内の SharePoint コマンドを実装するアセンブリの相対パスに設定します。 詳細については、「 [Asset 要素 (VSX Schema)](/previous-versions/dd393737(v=vs.110))」を参照してください。

    - 拡張機能にプロジェクトテンプレートまたは項目テンプレートが含まれている場合は、要素の下に要素 `ProjectTemplate` または要素を追加し `ItemTemplate` `Assets` ます。 新しい要素の値を、VSIX パッケージ内のテンプレートが格納されているフォルダーの相対パスに設定します。 詳細については、「 [Projecttemplate 要素 (VSX schema)](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\)) 」および「 [ITEMTEMPLATE 要素 (VSX schema)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))」を参照してください。

    - 拡張機能にプロジェクトテンプレートまたは項目テンプレートのカスタムウィザードが含まれている場合は、要素の下に要素を追加し `Assembly` `Assets` ます。 新しい要素の値を、VSIX パッケージ内のアセンブリの相対パスに設定し、 `AssemblyName` 属性を完全なアセンブリ名 (バージョン、カルチャ、公開キートークンを含む) に設定します。 詳細については、「 [Dependency 要素 (VSX Schema)](/previous-versions/dd393682(v=vs.110))」を参照してください。

### <a name="example"></a>例

次の例は、SharePoint ツールの拡張機能の source.extension.vsixmanifest ファイルの内容を示しています。 この拡張機能は Contoso.ProjectExtension.dll という名前のアセンブリに実装されています。 拡張機能には、Contoso.ExtensionCommands.dll という名前の SharePoint コマンドアセンブリと、VSIX パッケージで **Itemtemplates** という名前のフォルダーの下に項目テンプレートが含まれています。 この例では、両方のアセンブリが VSIX パッケージの source.extension.vsixmanifest ファイルと同じフォルダーにあることを前提としています。

```xml
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <Identity Id="CustomActionProjectItem.Microsoft.b99efe4d-cef3-4afd-b9af-034ca0c52743" Version="1.0" Language="en-US" Publisher="Microsoft" />
    <DisplayName>CustomActionProjectItem</DisplayName>
    <Description>Empty VSIX Project.</Description>
  </Metadata>
  <Installation>
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="11.0" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" Version="4.5" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.ItemTemplate" Path="ItemTemplates" />
    <Asset Type="Microsoft.VisualStudio.MefComponent" Path="ProjectItemDefinition.dll" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>関連項目

- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)