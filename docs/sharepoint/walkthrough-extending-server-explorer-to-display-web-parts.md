---
title: 'チュートリアル: Web パーツを表示するためのサーバーエクスプローラーの拡張 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 915a1762782b2bf7177b87a3a5f4cdc6e08c6405
ms.sourcegitcommit: 7a46232242783ebe23f2527f91eac8eb84b3ae05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90739994"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する
  Visual Studio では、**サーバーエクスプローラー**の [ **sharepoint 接続**] ノードを使用して、sharepoint サイトのコンポーネントを表示できます。 ただし、一部のコンポーネントは既定では **サーバーエクスプローラー** 表示されません。 このチュートリアルでは、接続されている各 SharePoint サイトに Web パーツギャラリーを表示するように **サーバーエクスプローラー** を拡張します。

 このチュートリアルでは、次のタスクについて説明します。

- 次の方法で **サーバーエクスプローラー** を拡張する Visual Studio 拡張機能を作成します。

  - 拡張機能により、**サーバーエクスプローラー**の各 SharePoint サイトノードの下に**Web パーツギャラリー**ノードが追加されます。 この新しいノードには、サイトの Web パーツギャラリー内の各 Web パーツを表す子ノードが含まれています。

  - 拡張機能は、Web パーツのインスタンスを表す新しい種類のノードを定義します。 この新しいノードタイプは、[新しい **Web パーツギャラリー** ] ノードの下にある子ノードの基礎となります。 新しい Web パーツノード型は、表示されている Web パーツに関する情報を [ **プロパティ** ] ウィンドウに表示します。 ノード型には、Web パーツに関連する他のタスクを実行するための開始点として使用できるカスタムショートカットメニュー項目も含まれています。

- 拡張機能アセンブリが呼び出す2つのカスタム SharePoint コマンドを作成します。 SharePoint コマンドは、SharePoint のサーバーオブジェクトモデルで Api を使用するために拡張機能アセンブリから呼び出すことができるメソッドです。 このチュートリアルでは、開発用コンピューターのローカル SharePoint サイトから Web パーツ情報を取得するコマンドを作成します。 詳細については、「 [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

- 拡張機能を配置するための Visual Studio Extension (VSIX) パッケージをビルドします。

- 拡張機能のデバッグとテスト。

> [!NOTE]
> サーバーオブジェクトモデルではなく、SharePoint 用のクライアントオブジェクトモデルを使用するこのチュートリアルの代替バージョンについては、「 [チュートリアル: サーバーエクスプローラー拡張機能での sharepoint クライアントオブジェクトモデルの呼び出し](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)」を参照してください。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポートされている Windows、SharePoint、および Visual Studio のエディション。

- Visual Studio SDK。 このチュートリアルでは、SDK の **Vsix プロジェクト** テンプレートを使用して、プロジェクト項目を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint のサーバーオブジェクトモデルの使用。 詳細については、「 [SharePoint Foundation Server 側のオブジェクトモデルの使用](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))」を参照してください。

- SharePoint ソリューションでの Web パーツ。 詳細については、「 [Web パーツの概要](/previous-versions/office/ms432401(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、次の3つのプロジェクトを作成する必要があります。

- 拡張機能を配置する VSIX パッケージを作成する VSIX プロジェクト。

- 拡張機能を実装するクラスライブラリプロジェクト。 このプロジェクトは、.NET Framework 4.5 をターゲットにする必要があります。

- カスタム SharePoint コマンドを定義するクラスライブラリプロジェクト。 このプロジェクトは .NET Framework 3.5 を対象にする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. [  **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **機能拡張** ] ノードを選択します。

    > [!NOTE]
    > **機能拡張**ノードは、VISUAL Studio SDK をインストールした場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

5. [ **VSIX プロジェクト** ] テンプレートを選択し、プロジェクトに **webpartnode**という名前を指定して、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**ソリューションエクスプローラー**に**webpartnode**プロジェクトを追加します。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューションエクスプローラー**で、ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows** ノードの選択] をクリックします。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

4. プロジェクトテンプレートの一覧で [ **クラスライブラリ**] を選択し、プロジェクトに **webpartnodeextension**という名前を指定して、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Webpartnodeextension**プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-commands-project"></a>SharePoint コマンド プロジェクトを作成するには

1. **ソリューションエクスプローラー**で、ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [  **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows** ] ノードをクリックします。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 3.5** ] を選択します。

4. プロジェクトテンプレートの一覧で [ **クラスライブラリ**] を選択し、プロジェクトに **webpartcommands**という名前を指定して、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Webpartcommands**プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 拡張機能を作成するコードを記述する前に、コードファイルとアセンブリ参照を追加し、プロジェクト設定を構成する必要があります。

#### <a name="to-configure-the-webpartnodeextension-project"></a>WebPartNodeExtension プロジェクトを構成するには

1. WebPartNodeExtension プロジェクトで、次の名前を持つ4つのコードファイルを追加します。

    - Sitモジュール Deextension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - Webpart・ Dids

2. **Webpartnodeextension**プロジェクトのショートカットメニューを開き、[参照の**追加**] を選択します。

3. [ **参照マネージャー-WebPartNodeExtension** ] ダイアログボックスで、[ **Framework** ] タブを選択し、次の各アセンブリのチェックボックスをオンにします。

    - System.ComponentModel.Composition

    - System.Windows.Forms

4. [ **拡張** ] タブを選択し、VisualStudio アセンブリのチェックボックスをオンにして、[ **OK** ] をクリックします。

5. **ソリューションエクスプローラー**で、[ **webpartnodeextension** ] プロジェクトノードのショートカットメニューを開き、[**プロパティ**] を選択します。

     **プロジェクト デザイナー**が開きます。

6. **[アプリケーション]** タブを選択します。

7. [ **既定の名前空間** ] ボックス (C#) または **ルート名前空間** ボックス ( [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ) で、「 **Serverexplorer. sharepointconnections. webpartnode**」と入力します。

#### <a name="to-configure-the-webpartcommands-project"></a>Webpartcommands プロジェクトを構成するには

1. WebPartCommands プロジェクトで、WebPartCommands という名前のコードファイルを追加します。

2. **ソリューションエクスプローラー**で、[ **webpartcommands** ] プロジェクトノードのショートカットメニューを開き、[**追加**]、[**既存の項目**] の順に選択します。

3. [ **既存項目の追加** ] ダイアログボックスで、WebPartNodeExtension プロジェクトのコードファイルが格納されているフォルダーを参照し、Webpartnodeextension コードファイルと webpartのコードファイルを選択します。

4. [ **追加** ] ボタンの横にある矢印をクリックし、表示されるメニューの [ **リンクとして追加** ] を選択します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] リンクとして、WebPartCommands プロジェクトにコードファイルを追加します。 その結果、コードファイルは WebPartNodeExtension プロジェクトに配置されますが、ファイル内のコードも WebPartCommands プロジェクトにコンパイルされます。

5. **Webpartcommands**プロジェクトのショートカットメニューをもう一度開き、[**参照の追加**] を選択します。

6. [ **参照マネージャー-WebPartCommands** ] ダイアログボックスで、[ **拡張機能** ] タブを選択し、次の各アセンブリのチェックボックスをオンにして、[ **OK** ] をクリックします。

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

7. **ソリューションエクスプローラー**で、 **webpartcommands**プロジェクトのショートカットメニューをもう一度開き、[**プロパティ**] を選択します。

     **プロジェクト デザイナー**が開きます。

8. **[アプリケーション]** タブを選択します。

9. [ **既定の名前空間** ] ボックス (C#) または **ルート名前空間** ボックス ( [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ) で、「 **Serverexplorer. sharepointconnections. webpartnode**」と入力します。

## <a name="create-icons-for-the-new-nodes"></a>新しいノードのアイコンを作成する
 **サーバーエクスプローラー**拡張機能用に2つのアイコンを作成します。新しい**web パーツギャラリー**ノード用のアイコンと、 **web パーツギャラリー**ノードの下にある子 Web パーツノードごとに別のアイコンを作成します。 このチュートリアルの後半では、これらのアイコンをノードに関連付けるコードを記述します。

#### <a name="to-create-icons-for-the-nodes"></a>ノードのアイコンを作成するには

1. **ソリューションエクスプローラー**で、 **webpartnodeextension**プロジェクトのショートカットメニューを開き、[**プロパティ**] を選択します。

2. **プロジェクト デザイナー**が開きます。

3. [ **リソース** ] タブを選択し、[ **このプロジェクトに既定のリソースファイルが含まれていません] を選択します。1つのリンクを作成するには、ここをクリックし** てください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] リソースファイルを作成し、デザイナーで開きます。

4. デザイナーの上部で、[ **リソースの追加** ] メニューコマンドの横にある矢印をクリックし、表示されるメニューで [ **新しいアイコンの追加** ] を選択します。

5. [ **新しいリソースの追加** ] ダイアログボックスで、新しいアイコン [ **webpartsnode**] に名前を指定し、[ **追加** ] ボタンを選択します。

     **イメージエディター**に新しいアイコンが表示されます。

6. アイコンの16x16 バージョンを編集して、簡単に認識できるデザインを作成します。

7. 32x32 バージョンのアイコンのショートカットメニューを開き、[ **イメージの種類の削除**] を選択します。

8. 手順 5. ~ 8. を繰り返して、プロジェクトリソースに2つ目のアイコンを追加し、このアイコン **WebPart**という名前を指定します。

9. **ソリューションエクスプローラー**で、 **webpartnodeextension**プロジェクトの**Resources**フォルダーの下にある [ **webpartnodeextension**] のショートカットメニューを開きます。

10. [ **プロパティ** ] ウィンドウで、[ **ビルドアクション**] の横にある矢印を選択し、表示されるメニューの [ **埋め込みリソース** ] をクリックします。

11. **WebPart**の最後の2つの手順を繰り返します。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツギャラリーノードをサーバーエクスプローラーに追加します。
 新しい **Web パーツギャラリー** ノードを各 SharePoint サイトノードに追加するクラスを作成します。 新しいノードを追加するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。 ノードに子ノードを追加するなど、 **サーバーエクスプローラー**の既存のノードの動作を拡張する場合は常に、このインターフェイスを実装します。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツギャラリーノードをサーバーエクスプローラーに追加するには

1. WebPartNodeExtension プロジェクトで、Sit"拡張機能" コードファイルを開き、次のコードを貼り付けます。

    > [!NOTE]
    > このコードを追加すると、プロジェクトのコンパイルエラーが発生しますが、後の手順でコードを追加したときに、そのエラーが解消されます。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]

## <a name="define-a-node-type-that-represents-a-web-part"></a>Web パーツを表すノードの種類を定義する
 Web パーツを表す新しい型のノードを定義するクラスを作成します。 Visual Studio では、この新しいノードタイプを使用して、 **Web パーツギャラリー** ノードの下に子ノードを表示します。 各子ノードは、SharePoint サイト上の1つの Web パーツを表します。

 新しいノード型を定義するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> ます。 **サーバーエクスプローラー**で新しい種類のノードを定義する場合は、常にこのインターフェイスを実装します。

#### <a name="to-define-the-web-part-node-type"></a>Web パーツノードの種類を定義するには

1. WebPartNodeExtension プロジェクトで、WebPartNodeTypeProvder コードファイルを開き、次のコードを貼り付けます。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs#2)]

## <a name="define-the-web-part-data-class"></a>Web パーツのデータクラスを定義する
 SharePoint サイトの1つの Web パーツに関するデータを含むクラスを定義します。 このチュートリアルの後半では、サイトの各 Web パーツに関するデータを取得し、このクラスのインスタンスにデータを割り当てるカスタム SharePoint コマンドを作成します。

#### <a name="to-define-the-web-part-data-class"></a>Web パーツのデータクラスを定義するには

1. WebPartNodeExtension プロジェクトで、Webpartnodeextension コードファイルを開き、次のコードを貼り付けます。

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb#3)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs#3)]

## <a name="define-the-ids-for-the-sharepoint-commands"></a>SharePoint コマンドの Id を定義します。
 カスタム SharePoint コマンドを識別する複数の文字列を定義します。 これらのコマンドは、このチュートリアルの後半で実装します。

#### <a name="to-define-the-command-ids"></a>コマンド Id を定義するには

1. WebPartNodeExtension プロジェクトで、Webpartのコードファイルを開き、次のコードを貼り付けます。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs#4)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb#4)]

## <a name="create-the-custom-sharepoint-commands"></a>カスタム SharePoint コマンドを作成する
 Sharepoint のサーバーオブジェクトモデルを呼び出すカスタムコマンドを作成して、SharePoint サイトの Web パーツに関するデータを取得します。 各コマンドは、が適用されたメソッドです <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. WebPartCommands プロジェクトで、WebPartCommands コードファイルを開き、次のコードを貼り付けます。

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs#6)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb#6)]

## <a name="checkpoint"></a>Checkpoint
 このチュートリアルのこの時点で、 **Web パーツギャラリー** ノードと SharePoint コマンドのすべてのコードがプロジェクトに含まれるようになりました。 ソリューションをビルドして、両方のプロジェクトがエラーなしでコンパイルされるようにします。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

    > [!WARNING]
    > この時点では、WebPartNode プロジェクトのビルドエラーが発生する可能性があります。これは、VSIX マニフェストファイルに Author の値がないためです。 このエラーは、後の手順で値を追加したときに解消されます。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージの作成
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、vsix プロジェクトの source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-the-vsix-package"></a>VSIX パッケージを構成するには

1. **ソリューションエクスプローラー**の [webpartnode] プロジェクトの下で、マニフェストエディターで**source.extension.vsixmanifest**ファイルを開きます。

     source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. [ **製品名** ] ボックスに、 **サーバーエクスプローラーの Web パーツギャラリーノード**を入力します。

3. [ **作成者** ] ボックスに「 **Contoso**」と入力します。

4. [ **説明** ] ボックスに「」と入力して、 **[サーバーエクスプローラーの [SharePoint 接続] ノードに [カスタム Web パーツギャラリー] ノードを追加します。この拡張機能では、カスタム SharePoint コマンドを使用して、サーバーオブジェクトモデルを呼び出します。**

5. エディターの [ **アセット** ] タブを選択し、[ **新規作成** ] をクリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

6. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. [  **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト**を選択します。

8. [ **プロジェクト** ] ボックスの一覧で [ **webpartnodeextension** ] を選択し、[ **OK** ] をクリックします。

9. マニフェストエディターで、[ **新規作成** ] ボタンをもう一度クリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

10. [ **種類** ] ボックスに「 **SharePoint. コマンド. v4**」と入力します。

    > [!NOTE]
    > この要素は、Visual Studio 拡張機能に追加するカスタム拡張機能を指定します。 詳細については、「 [Asset 要素 (VSX Schema)](/previous-versions/dd393737(v=vs.110))」を参照してください。

11. [ **ソース** ] ボックスの一覧で、[現在のソリューションリスト項目 **内のプロジェクト** ] を選択します。

12. [ **プロジェクト** ] ボックスの一覧で [ **webpartcommands**] を選択し、[ **OK** ] をクリックします。

13. メニューバーで [ビルド] [ソリューションの**ビルド**] の順に選択し、  >  **Build Solution**ソリューションがエラーなしでコンパイルされることを確認します。

14. WebPartNode プロジェクトのビルド出力フォルダーに、WebPartNode .vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-extension"></a>拡張機能をテストする
 これで、**サーバーエクスプローラー**で新しい**Web パーツギャラリー**ノードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで拡張機能のデバッグを開始します。 次に、の実験用インスタンスの [新しい **Web パーツ** ] ノードを使用し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]管理者資格情報で再起動し、WebPartNode ソリューションを開きます。

2. WebPartNodeExtension プロジェクトで、Sit\n Deextension コードファイルを開き、メソッドとメソッドの最初のコード行にブレークポイントを追加し `NodeChildrenRequested` `CreateWebPartNodes` ます。

3. F5 キーを **押し** てデバッグを開始します。

     Visual Studio によって、サーバー Explorer\1.0 の%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part Gallery ノード拡張機能がインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. の実験用インスタンスの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メニューバーで、[サーバーエクスプローラーの**表示**] を選択し  >  **Server Explorer**ます。

2. テストに使用する SharePoint サイトが**サーバーエクスプローラー**の [ **sharepoint 接続**] ノードに表示されない場合は、次の手順を実行します。

    1. **サーバーエクスプローラー**で、[ **SharePoint 接続**] のショートカットメニューを開き、[**接続の追加**] を選択します。

    2. [ **Sharepoint 接続の追加** ] ダイアログボックスで、接続先の sharepoint サイトの URL を入力し、[ **OK** ] をクリックします。

         開発用コンピューターで SharePoint サイトを指定するには、「」と入力し **http://localhost** ます。

3. サイトの接続ノード (サイトの URL が表示されます) を展開し、子サイトノード (たとえば、[ **チームサイト**]) を展開します。

4. のもう一方のインスタンスのコードが、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メソッドで前に設定したブレークポイントで停止していることを確認 `NodeChildrenRequested` し、 **F5 キー** を押してプロジェクトのデバッグを続行します。

5. Visual Studio の実験用インスタンスで、[ **Web パーツギャラリー** ] という名前の新しいノードが最上位サイトノードの下に表示されていることを確認し、[ **web パーツギャラリー** ] ノードを展開します。

6. Visual Studio のもう一方のインスタンスのコードが、メソッドで前に設定したブレークポイントで停止していることを確認 `CreateWebPartNodes` し、 **F5** キーを押してプロジェクトのデバッグを続行します。

7. Visual Studio の実験用インスタンスで、接続されたサイトのすべての Web パーツが**サーバーエクスプローラー**の [ **Web パーツギャラリー** ] ノードの下に表示されていることを確認します。

8. **サーバーエクスプローラー**で、Web パーツの1つのショートカットメニューを開き、[**プロパティ**] を選択します。

9. デバッグしているのインスタンスで、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Web パーツの詳細が [ **プロパティ** ] ウィンドウに表示されていることを確認します。

## <a name="uninstall-the-extension-from-visual-studio"></a>Visual Studio から拡張機能をアンインストールする
 拡張機能のテストが完了したら、Visual Studio から拡張機能をアンインストールします。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. の実験用インスタンスの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、 **サーバーエクスプローラーの [Web パーツギャラリー] ノード拡張**を選択し、[ **アンインストール** ] をクリックします。

3. 表示されるダイアログボックスで、[ **はい** ] をクリックして拡張機能をアンインストールすることを確認し、[ **今すぐ再起動** ] ボタンをクリックしてアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験用インスタンスと、WebPartNode ソリューションが開いている Visual Studio のインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバーエクスプローラーの拡張機能で SharePoint クライアントオブジェクトモデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [アイコン用イメージエディター](/cpp/windows/image-editor-for-icons)
- [アイコンまたはその他のイメージを作成するアイコンのイメージエディター &#40;&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)