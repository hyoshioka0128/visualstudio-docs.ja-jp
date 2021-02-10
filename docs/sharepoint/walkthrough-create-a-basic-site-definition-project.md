---
title: 'チュートリアル: 基本的なサイト定義プロジェクトの作成 |Microsoft Docs'
description: この SharePoint チュートリアルでは、「いくつかのコントロールを持つ視覚的な Web パーツを含む基本的なサイト定義を作成する方法」を参照してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: def1ae862a7b9ba4def62cb590260c5a18758929
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937707"
---
# <a name="walkthrough-create-a-basic-site-definition-project"></a>チュートリアル: 基本的なサイト定義プロジェクトの作成
  このチュートリアルでは、いくつかのコントロールを含む視覚的 Web パーツを含む基本的なサイト定義を作成する方法について説明します。 わかりやすくするために、作成する視覚的 Web パーツにはいくつかのコントロールしかありません。 ただし、より高度な SharePoint サイト定義を作成して、より多くの機能を含めることができます。

 このチュートリアルでは、次のタスクについて説明します。

- プロジェクトテンプレートを使用してサイト定義を作成する [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- Sharepoint でサイト定義を使用して SharePoint サイトを作成する。

- ビジュアル Web パーツをソリューションに追加します。

- 新しいビジュアル Web パーツを追加して、サイトの default.aspx ページをカスタマイズする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。 詳細については、「SharePoint ソリューションを開発するための要件」を参照してください。

- 見ることができます。

## <a name="create-a-site-definition-solution"></a>サイト定義ソリューションを作成する
 まず、でサイト定義プロジェクトを作成し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

#### <a name="to-create-a-site-definition-project"></a>サイト定義プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、メニューバーで [**ファイル**] [新規作成] [プロジェクト] の順に選択し  >  ます。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [ **Visual C#** ] ノードまたは **[Visual Basic** ] ノードを展開し、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

3. [ **テンプレート** ] ボックスの一覧で、[ **SharePoint 2010] プロジェクト** テンプレートを選択します。

4. [ **名前** ] ボックスに「 **testsitedef**」と入力し、[ **OK** ] をクリックします。

    **SharePoint カスタマイズウィザード** が表示されます。

5. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、サイト定義をデバッグする SharePoint サイトの URL を入力するか、既定の場所 (Http://<em>システム名</em>/) を使用します。

6. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、[ **ファームソリューションとして配置** する] オプションボタンを選択します。

    すべてのサイト定義プロジェクトは、ファームソリューションとして配置する必要があります。 サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックします。

    プロジェクトが **ソリューションエクスプローラー** に表示されます。

8. **ソリューションエクスプローラー** で、プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

9. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

10. [ **テンプレート** ] ペインで、[ **サイト定義** ] テンプレートを選択し、 **名前** は **SiteDefinition1** のままにして、[ **追加** ] ボタンを選択します。

## <a name="create-a-visual-web-part"></a>視覚的 web パーツを作成する
 次に、サイト定義のメインページに表示する視覚的 Web パーツを作成します。

#### <a name="to-create-a-visual-web-part"></a>視覚的 web パーツを作成するには

1. **ソリューションエクスプローラー** で、[**すべてのファイルを表示**] ボタンをクリックします。

2. **SiteDefinition1** プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

3. [ **Visual C#** ] ノードまたは **[Visual Basic** ] ノードを展開し、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

4. テンプレートの一覧で [ **Visual Web パーツ** ] テンプレートを選択し、既定の名前 VisualWebPart1 をそのままにして、[ **追加** ] ボタンを選択します。

     *VisualWebPart1* ファイルが開きます。

5. *VisualWebPart1* の下部で、次のマークアップを追加して、テキストボックス、ボタン、およびラベルの3つのコントロールをフォームに追加します。

    ```aspx-csharp
    <table>
      <tr>
        <td>
          <asp:TextBox runat="server" ID="tbName"></asp:TextBox>
        </td>
        <td>
          <asp:Button runat="server" ID="btnSubmit" Text = "Change Label Text" OnClick="btnSubmit_Click"></asp:Button>
        </td>
        <td>
          <asp:Label runat="server" ID="lblName"></asp:Label>
        </td>
      </tr>
    </table>
    ```

6. *VisualWebPart1* の下で、 *VisualWebPart1.ascx.cs* ファイル (の場合) [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] または *VisualWebPart1* (の場合) を開き、 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 次のコードを追加します。

     [!code-vb[SP_SimpleSiteDef#1](../sharepoint/codesnippet/VisualBasic/testsitedefvb/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_SimpleSiteDef#1](../sharepoint/codesnippet/CSharp/testsitedef/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

     このコードは、web パーツのボタンクリック用の機能を追加します。

## <a name="add-the-visual-web-part-to-the-default-aspx-page"></a>既定の ASPX ページに視覚的 web パーツを追加する
 次に、視覚的 Web パーツをサイト定義の既定の ASPX ページに追加します。

#### <a name="to-add-a-visual-web-part-to-the-default-aspx-page"></a>既定の ASPX ページに視覚的 web パーツを追加するには

1. Default.aspx ページを開き、タグの下に次の行を追加し `WebPartPages` ます。

    ```aspx-csharp
    <%@ Register Tagprefix="MyWebPartControls" Namespace="TestSiteDef.VisualWebPart1" Assembly="$SharePoint.Project.AssemblyFullName$" %>
    ```

     この行によって、MyWebPartControls という名前が Web パーツとそのコードに関連付けられます。 *Namespace* パラメーターは、 *VisualWebPart1* コードファイルで使用されている名前空間と一致します。

2. 要素の後 `</asp:Content>` に、セクション全体 `ContentPlaceHolderId="PlaceHolderMain"` とその内容を次のコードに置き換えます。

    ```aspx-csharp
    <asp:Content ID="Content1" ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <MyWebPartControls:VisualWebPart1 runat="server" />
    </asp:Content>
    ```

     このコードは、前に作成したビジュアル Web パーツへの参照を作成します。

3. **ソリューションエクスプローラー** で、[ **SiteDefinition1** ] ノードのショートカットメニューを開き、[**スタートアップ項目に設定**] をクリックします。

## <a name="deploy-and-run-the-site-definition-solution"></a>サイト定義ソリューションを展開して実行する
 次に、プロジェクトを SharePoint に配置してから、プロジェクトを実行します。

#### <a name="to-deploy-and-run-the-site-definition"></a>サイト定義を配置して実行するには

- メニューバーで、[ **Build**  >  **Deploy testsitedef**] を選択します。

- **F5** キーを押します。

     Visual Studio は、コードをコンパイルし、その機能を追加し、すべてのファイルを SharePoint ソリューション (WSP) ファイルにパッケージ化して、WSP ファイルを SharePoint サーバーに配置します。 その後、SharePoint によってファイルがインストールされ、機能がアクティブ化されます。

## <a name="create-a-site-based-on-the-site-definition"></a>サイト定義に基づいてサイトを作成する
 次に、新しいサイト定義を使用してサイトを作成します。

#### <a name="to-create-a-site-by-using-the-site-definition"></a>サイト定義を使用してサイトを作成するには

1. SharePoint サイトで、[新しい SharePoint サイト] ページが表示されます。

2. [ **タイトルと説明** ] セクションで、タイトルとサイトの説明に **新しいサイト** を入力します。

3. [ **Web サイトのアドレス**] セクションで、[ **URL 名**] ボックスに「 **mynewsite** 」と入力します。

4. [ **テンプレート** ] セクションで、[ **SharePoint のカスタマイズ** ] タブを選択します。

5. **[テンプレートの選択**] の一覧で [ **SiteDefinition1**] を選択します。

6. その他の設定は既定値のままにして、[ **作成** ] ボタンをクリックします。

     新しいサイトが表示されます。

## <a name="test-the-new-site"></a>新しいサイトをテストする
 次に、新しいサイトをテストして、正常に動作するかどうかを確認します。

#### <a name="to-test-the-new-site"></a>新しいサイトをテストするには

- 既定の ASPX ページで、テキストを入力し、テキストボックスの横にある [ **ラベルテキストの変更** ] ボタンをクリックします。

     テキストは、ボタンの右側のラベルに表示されます。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
