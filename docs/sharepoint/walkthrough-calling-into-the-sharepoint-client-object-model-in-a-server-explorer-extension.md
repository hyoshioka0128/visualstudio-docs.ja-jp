---
title: 'サーバーエクスプローラー: SharePoint 接続ノードの拡張'
titleSuffix: ''
description: このチュートリアルでは、サーバーエクスプローラーの [SharePoint 接続] ノードの拡張機能から SharePoint クライアントオブジェクトモデルを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint commands [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dee53642e042c8d4db88bdba7c093f327527798d
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217022"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>チュートリアル: サーバーエクスプローラー拡張機能での SharePoint クライアントオブジェクトモデルの呼び出し
  このチュートリアルでは、**サーバーエクスプローラー** の [ **sharepoint 接続** ノードの拡張機能から sharepoint クライアントオブジェクトモデルを呼び出す方法について説明します。 SharePoint クライアントオブジェクトモデルの使用方法の詳細については、「 [sharepoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- 次の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 方法で **サーバーエクスプローラー** の **SharePoint 接続** ノードを拡張する拡張機能を作成します。

  - 拡張機能により、**サーバーエクスプローラー** の各 SharePoint サイトノードの下に **Web パーツギャラリー** ノードが追加されます。 この新しいノードには、サイトの Web パーツギャラリー内の各 Web パーツを表す子ノードが含まれています。

  - 拡張機能は、Web パーツのインスタンスを表す新しい種類のノードを定義します。 この新しいノードタイプは、[新しい **Web パーツギャラリー** ] ノードの下にある子ノードの基礎となります。 新しい Web パーツノード型では、ノードが表す Web パーツに関する情報が [ **プロパティ** ] ウィンドウに表示されます。

- 拡張機能を配置するための Visual Studio Extension (VSIX) パッケージをビルドします。

- 拡張機能のデバッグとテスト。

> [!NOTE]
> このチュートリアルで作成する拡張機能は、 [「チュートリアル: web パーツを表示するためのサーバーエクスプローラーの拡張](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」で作成した拡張機能に似ています。 このチュートリアルでは、SharePoint サーバーオブジェクトモデルを使用しますが、このチュートリアルでは、クライアントオブジェクトモデルを使用して同じタスクを行います。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、SDK の **Vsix プロジェクト** テンプレートを使用して、拡張機能を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint クライアントオブジェクトモデルの使用。 詳細については、「管理された [クライアントオブジェクトモデル](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))」を参照してください。

- SharePoint の Web パーツ。 詳細については、「 [Web パーツの概要](/previous-versions/office/ms432401(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、次の2つのプロジェクトを作成する必要があります。

- **サーバーエクスプローラー** 拡張機能を配置する vsix パッケージを作成する vsix プロジェクト。

- **サーバーエクスプローラー** 拡張機能を実装するクラスライブラリプロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **機能拡張**] を選択します。

    > [!NOTE]
    > **機能拡張** ノードは、VISUAL Studio SDK をインストールした場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

     SharePoint ツール拡張機能には、このバージョンの .NET Framework の機能が必要です。

5. [ **VSIX プロジェクト** ] テンプレートを選択します。

6. [ **名前** ] ボックスに「 **webpartnode**」と入力し、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**ソリューションエクスプローラー** に **webpartnode** プロジェクトを追加します。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューションエクスプローラー** で、ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [  **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows**] を選択します。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

4. プロジェクトテンプレートの一覧で、[ **クラスライブラリ**] を選択します。

5. [ **名前** ] ボックスに「 **webpartnodeextension**」と入力し、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Webpartnodeextension** プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

6. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-extension-project"></a>拡張機能プロジェクトの構成
 拡張機能を作成するコードを記述する前に、コードファイルとアセンブリ参照をプロジェクトに追加する必要があります。また、既定の名前空間を更新する必要があります。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. **Webpartnodeextension** プロジェクトで、Sitare Deextension と WebPartNodeTypeProvider という名前の2つのコードファイルを追加します。

2. WebPartNodeExtension プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択します。

3. [ **参照マネージャー-WebPartNodeExtension** ] ダイアログボックスで、[ **フレームワーク** ] ノードを選択し、system.componentmodel アセンブリおよび system.string アセンブリのチェックボックスをオンにします。

4. [ **拡張機能** ] ノードを選択し、次の各アセンブリのチェックボックスをオンにして、[ **OK** ] をクリックします。

    - Microsoft. SharePoint. Client

    - Microsoft. SharePoint. Client. Runtime

    - Microsoft.VisualStudio.SharePoint

5. **Webpartnodeextension** プロジェクトのショートカットメニューを開き、[**プロパティ**] を選択します。

     **プロジェクト デザイナー** が開きます。

6. **[アプリケーション]** タブを選択します。

7. [ **既定の名前空間** ] ボックス (C#) または [ **ルート名前空間** ] ボックス (Visual Basic) で、「 **Serverexplorer. sharepointconnections. webpartnode**」と入力します。

## <a name="create-icons-for-the-new-nodes"></a>新しいノードのアイコンを作成する
 **サーバーエクスプローラー** 拡張機能用に2つのアイコンを作成します。新しい **web パーツギャラリー** ノードのアイコンと、 **web パーツギャラリー** ノードの下にある子 Web パーツノードごとに別のアイコンがあります。 このチュートリアルの後半では、これらのアイコンをノードに関連付けるコードを記述します。

#### <a name="to-create-icons-for-the-nodes"></a>ノードのアイコンを作成するには

1. WebPartNodeExtension プロジェクトの **プロジェクトデザイナー** で、[ **リソース** ] タブを選択します。

2. **このプロジェクトに既定のリソースファイルが含まれていないリンクを選択します。ここをクリックして作成します。**

     Visual Studio によってリソースファイルが作成され、デザイナーで開かれます。

3. デザイナーの上部で、[ **リソースの追加** ] メニューコマンドの矢印をクリックし、[ **新しいアイコンの追加**] を選択します。

4. 新しいアイコン名として「 **Webpartsnode** 」と入力し、[ **追加** ] ボタンを選択します。

     **イメージエディター** に新しいアイコンが表示されます。

5. アイコンの16x16 バージョンを編集して、簡単に認識できるデザインを作成します。

6. 32x32 バージョンのアイコンのショートカットメニューを開き、[ **イメージの種類の削除**] を選択します。

7. 手順 3. ~ 7. を繰り返して、プロジェクトリソースに2つ目のアイコンを追加し、このアイコン **WebPart** という名前を指定します。

8. **ソリューションエクスプローラー**、 **webpartnodeextension** プロジェクトの **Resources** フォルダーで、[ *webpartnodeextension*] を選択します。

9. [ **プロパティ** ] ウィンドウで、[ **ビルドアクション** ] ボックスの一覧を開き、[ **埋め込みリソース**] を選択します。

10. *WebPart* の最後の2つの手順を繰り返します。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツギャラリーノードをサーバーエクスプローラーに追加します。
 新しい **Web パーツギャラリー** ノードを各 SharePoint サイトノードに追加するクラスを作成します。 新しいノードを追加するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。 新しい子ノードをノードに追加するなど、 **サーバーエクスプローラー** の既存のノードの動作を拡張する場合は常に、このインターフェイスを実装します。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツギャラリーノードをサーバーエクスプローラーに追加するには

1. 次のコードを、 **Webpartnodeextension** プロジェクトの **sitモジュール deextension** コードファイルに貼り付けます。

    > [!NOTE]
    > このコードを追加した直後は、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>Web パーツを表すノードの種類を定義する
 Web パーツを表す新しい型のノードを定義するクラスを作成します。 Visual Studio では、この新しいノードタイプを使用して、 **Web パーツギャラリー** ノードの下に子ノードを表示します。 これらの各子ノードは、SharePoint サイト上の1つの Web パーツを表します。

 新しいノード型を定義するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> ます。 **サーバーエクスプローラー** で新しい種類のノードを定義する場合は、常にこのインターフェイスを実装します。

#### <a name="to-define-the-web-part-node-type"></a>Web パーツノードの種類を定義するには

1. 次のコードを、 **Webpartnodeextension** プロジェクトの **Webpartnodetypeprovider** コードファイルに貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::

## <a name="checkpoint"></a>Checkpoint
 このチュートリアルのこの時点で、 **Web パーツギャラリー** ノードのすべてのコードがプロジェクト内にあります。 **Webpartnodeextension** プロジェクトをビルドして、エラーが発生せずにコンパイルされるようにします。

#### <a name="to-build-the-project"></a>プロジェクトをビルドするには

1. **ソリューションエクスプローラー** で、 **webpartnodeextension** プロジェクトのショートカットメニューを開き、[**ビルド**] を選択します。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージの作成
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-the-vsix-package"></a>VSIX パッケージを構成するには

1. **ソリューションエクスプローラー** の [ **webpartnode** ] プロジェクトで、マニフェストエディターの **source.extension.vsixmanifest** ファイルを開きます。

     source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. [ **製品名** ] ボックスに、 **サーバーエクスプローラーの Web パーツギャラリーノード** を入力します。

3. [ **作成者** ] ボックスに「 **Contoso**」と入力します。

4. [ **説明** ] ボックスに「」と入力して、 **[サーバーエクスプローラーの [SharePoint 接続] ノードに [カスタム Web パーツギャラリー] ノードを追加** します。

5. エディターの [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。

6. [ **新しい資産の追加** ] ダイアログボックスの [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** を選択します。

8. [ **プロジェクト** ] ボックスの一覧で [ **webpartnodeextension**] を選択し、[ **OK** ] をクリックします。

9. メニューバーで [ビルド] [ソリューションの **ビルド**] の順に選択し、  >  ソリューションがエラーなしでコンパイルされることを確認します。

10. WebPartNode プロジェクトのビルド出力フォルダーに、WebPartNode .vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-extension"></a>拡張機能をテストする
 これで、**サーバーエクスプローラー** で新しい **Web パーツギャラリー** ノードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで拡張機能プロジェクトのデバッグを開始します。 次に、Visual Studio の実験用インスタンスの [新しい **Web パーツ** ] ノードを使用します。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 管理者資格情報を使用して Visual Studio を再起動し、 **Webpartnode** ソリューションを開きます。

2. WebPartNodeExtension プロジェクトで、 **Sit\n deextension** コードファイルを開き、メソッドとメソッドの最初のコード行にブレークポイントを追加し `NodeChildrenRequested` `CreateWebPartNodes` ます。

3. F5 キーを **押し** てデバッグを開始します。

     Visual Studio によって、サーバー Explorer\1.0 の%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part Gallery ノード拡張機能がインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. Visual Studio の実験用インスタンスのメニューバーで、[サーバーエクスプローラーの **表示**] を選択し  >  ます。

2. テストに使用する SharePoint サイトが **サーバーエクスプローラー** の [ **sharepoint 接続**] ノードの下に表示されていることを確認します。 一覧に表示されていない場合は、次の手順を実行します。

    1. **SharePoint 接続** のショートカットメニューを開き、[**接続の追加**] を選択します。

    2. [ **Sharepoint 接続の追加** ] ダイアログボックスで、接続先の sharepoint サイトの URL を入力し、[ **OK** ] をクリックします。

         開発用コンピューターで SharePoint サイトを指定するには、「」と入力 **http://localhost** します。

3. サイトの接続ノード (サイトの URL が表示されます) を展開し、子サイトノード (たとえば、[ **チームサイト**]) を展開します。

4. Visual Studio のもう一方のインスタンスのコードが、メソッドで前に設定したブレークポイントで停止していることを確認 `NodeChildrenRequested` し、 **F5** キーを押してプロジェクトのデバッグを続行します。

5. Visual Studio の実験用インスタンスで、最上位サイトノードの下に表示される [ **Web パーツギャラリー** ] ノードを展開します。

6. Visual Studio のもう一方のインスタンスのコードが、メソッドで前に設定したブレークポイントで停止していることを確認 `CreateWebPartNodes` し、 **F5** キーを押してプロジェクトのデバッグを続行します。

7. Visual Studio の実験用インスタンスで、接続されたサイトのすべての Web パーツが **サーバーエクスプローラー** の [ **Web パーツギャラリー** ] ノードの下に表示されていることを確認します。

8. Web パーツのショートカットメニューを開き、[ **プロパティ**] をクリックします。

9. [ **プロパティ** ] ウィンドウで、Web パーツの詳細が表示されていることを確認します。

10. **サーバーエクスプローラー** で、同じ Web パーツのショートカットメニューを開き、[メッセージの **表示**] を選択します。

     表示されるメッセージボックスで、[ **OK** ] をクリックします。

## <a name="uninstall-the-extension-from-visual-studio"></a>Visual Studio から拡張機能をアンインストールする
 拡張機能のテストが完了したら、Visual Studio からアンインストールします。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、[ **サーバーエクスプローラー] の [Web パーツギャラリー] ノード** を選択し、[ **アンインストール** ] をクリックします。

3. 表示されるダイアログボックスで、[ **はい** ] をクリックします。

4. [ **今すぐ再起動** ] ボタンをクリックして、アンインストールを完了します。

     プロジェクト項目もアンインストールされます。

5. Visual Studio の両方のインスタンス (実験用インスタンスと、WebPartNode ソリューションが開いている Visual Studio のインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)
- [アイコンまたはその他のイメージを作成するアイコンのイメージエディター &#40;&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)