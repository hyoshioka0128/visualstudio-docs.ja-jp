---
title: SharePoint 用の Web パーツを作成する |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- Microsoft.SharePoint.WebControls.DateTimeControl
- Microsoft.SharePoint.WebControls.CssLink
- Microsoft.SharePoint.WebControls.RssLink
- Microsoft.SharePoint.WebControls.Theme
- Microsoft.SharePoint.WebControls.AspMenu
- Microsoft.SharePoint.WebControls.ListProperty
- Microsoft.SharePoint.WebControls.ProjectProperty
- Microsoft.SharePoint.WebControls.FormsDigest
- Microsoft.SharePoint.WebControls.ScriptLink
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web Parts
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3825ef7d2c1c90f63a90f5028063c74332543841
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015052"
---
# <a name="create-web-parts-for-sharepoint"></a>SharePoint の web パーツの作成
  Web パーツを作成すると、SharePoint サイト ページのコンテンツ、外観、および動作をユーザーがブラウザーから変更できます。 Web パーツは、Web パーツ ページ内で実行されるサーバー側コントロールです。SharePoint サイトに表示されるページはこれらの Web パーツで構成されます。 「[ビルディングブロック: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

 SharePoint サイトの Web パーツを作成およびデバッグするには、Visual Studio のテンプレートを使用します。

## <a name="create-a-web-part-in-visual-studio"></a>Visual Studio で web パーツを作成する
 **Web パーツ項目を**SharePoint プロジェクトに追加して、web パーツを作成します。 サンドボックスソリューションまたはファームソリューションで**Web パーツ**項目を使用できます。

 デザイナーを使用して web パーツを視覚的にデザインする場合は、**視覚的 Web パーツ**プロジェクトを作成するか、任意の SharePoint プロジェクトに**視覚的 web パーツ**項目を追加します。 **ビジュアル Web パーツ**項目は、ファームソリューションでのみ使用できます。

### <a name="web-part-item"></a>Web パーツ項目
 **Web パーツ**項目には、SharePoint サイトの web パーツをデザインするために使用できるファイルが用意されています。 **Web パーツ**項目を追加すると、Visual Studio によってプロジェクトにフォルダーが作成され、フォルダーに複数のファイルが追加されます。 各ファイルの説明を次の表に示します。

|ファイル|説明|
|----------|-----------------|
|*Elements.xml*|Web パーツを配置する際、プロジェクトのフィーチャー定義ファイルで使用する情報が格納されます。|
|.webpart ファイル|SharePoint の Web パーツ ギャラリーに Web パーツを表示するために必要な情報を指定します。|
|コード ファイル|Web パーツにコントロールを追加するメソッド、および Web パーツ内にカスタム コンテンツを生成するメソッドが保存されます。|

 詳細については、「[方法: SharePoint web パーツを作成](../sharepoint/how-to-create-a-sharepoint-web-part.md)する」を参照してください。

### <a name="visual-web-part-item"></a>視覚的 web パーツ項目
 視覚的 Web パーツは、Visual Studio の Visual Web Developer デザイナーを使用して作成する Web パーツです。 視覚的 Web パーツの機能は他の Web パーツと同じです。 ボタンやテキスト ボックスなどのコントロールを Web パーツに追加するときは、XML ファイルにコードを追加します。 ただし、ビジュアル web パーツにコントロールを追加するには、visual Studio の [**ツールボックス**] から web パーツにコントロールをドラッグまたはコピーします。 その後、XML ファイルで必要なコードを生成します。 「[方法: デザイナーを使用して SharePoint web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)」を参照してください。

## <a name="sharepoint-controls"></a>SharePoint コントロール
 Visual Studio には、アプリケーションのページなど、SharePoint ページを作成するためのコントロールが用意されています。 これらのコントロールは、[**ツールボックス**] の [ **SharePoint コントロール**] の下に表示されます。 これらのコントロールの機能は、 [WebControls](/previous-versions/office/sharepoint-server/ms413880(v=office.15))名前空間から派生します。この名前空間には、sharepoint サイトおよびリストページで使用される ASP.NET サーバーコントロールが含まれています。

|コントロール名|説明|
|------------------|-----------------|
|[AspMenu](/previous-versions/office/sharepoint-server/ms454108(v=office.15))|ASP メニューを挿入します。 詳細については、「[メニューコントロールの概要](/previous-versions/ecs0x9w5(v=vs.140))」を参照してください。|
|[CssLink](/previous-versions/office/sharepoint-server/ms439048(v=office.15))|*.Aspx*ページに**LINK**要素を挿入し、 **CssRegistration**で定義されている1つ以上の外部スタイルシートを適用します。|
|[DateTimeControl](/previous-versions/office/sharepoint-server/ms414993(v=office.15))|*.Aspx*ページに DateTime コントロールを挿入します。|
|[FormDigest](/previous-versions/office/sharepoint-server/ms416616(v=office.15))|.Aspx ページにセキュリティ検証を挿入し*ます。*|
|[ListProperty](/previous-versions/office/sharepoint-server/ms455032(v=office.15))|指定されたリストのプロパティを返します。|
|[ProjectProperty](/previous-versions/office/sharepoint-server/ms478990(v=office.15))|現在の Web サイトのグローバル プロパティを返します。|
|[.Rsslink](/previous-versions/office/sharepoint-server/ms457574(v=office.15))|RSS フィードへのリンクを *.aspx*ページに挿入します。|
|[ScriptLink](/previous-versions/office/sharepoint-server/ms411959(v=office.15))|スクリプトなどのリソースをページに登録し、ページのレンダリング時に要求できるようにするためのプロパティとメソッドを提供します。|
|[テーマ](/previous-versions/office/sharepoint-server/ms460735(v=office.15))|*.Aspx*ページにテーマを適用します。|

## <a name="debug-a-web-part"></a>Web パーツのデバッグ
 他の Visual Studio プロジェクトをデバッグする場合と同様に、Web パーツを含む SharePoint プロジェクトをデバッグできます。 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 コードのデバッグを開始するには、SharePoint で Web パーツ ページに Web パーツを追加します。

 SharePoint プロジェクトをデバッグする方法の詳細については、「 [sharepoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="visual-web-part-limitations"></a>視覚的 web パーツの制限事項
 Visual Studio では、SharePoint のサンドボックス ソリューションおよびファーム ソリューションに視覚的 Web パーツを追加できます。 ただし、視覚的 Web パーツには次のような制限があります。

- 視覚的 web パーツは、置換可能なパラメーターをサポートしていません。 詳細については、「[置換可能なパラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

- ユーザー コントロールと視覚的 Web パーツは、視覚的 Web パーツ上にドラッグ アンド ドロップしたり、コピーしたりできません。 これらの操作を実行するとビルド エラーが発生します。

- 視覚的 Web パーツは、$SPUrl などの SharePoint サーバー トークンを直接サポートしません。 詳細については、「 [SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」の「サンドボックス化されたビジュアル Web パーツでのトークン制限」を参照してください。

- サンドボックス ソリューションの視覚的 Web パーツは、"Sandboxed Code Host Service がビジー状態で要求を処理できなかったので、セキュリティで保護されたコード実行要求が拒否されました" というエラーが発生する場合があります。 このエラーの詳細については、 [SharePoint 開発者チームのブログ](https://blogs.msdn.microsoft.com/sharepointdev/2011/02/08/error-the-sandboxed-code-execution-request-was-refused-because-the-sandboxed-code-host-service-was-too-busy-to-handle-the-request-ricky-kirkham/#10149157)でこの投稿を参照してください。

- Visual Studio では、サーバー側 JavaScript のデバッグがサポートされていません。ただし、クライアント側 JavaScript のデバッグはサポートされています。

   サーバー側のマークアップ ファイルにインライン JavaScript を追加できますが、マークアップに追加したブレークポイントはデバッグできません。 JavaScript をデバッグするには、マークアップ ファイルで外部の JavaScript ファイルを参照し、JavaScript ファイルにブレークポイントを設定します。

- インライン [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] コードのデバッグは、マークアップ ファイルではなく、生成されたコード ファイルで実行する必要があります。

- 視覚的 Web パーツでは、`<@ Assembly Src=` ディレクティブを使用できません。

- SharePoint の Web コントロールと一部の [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] コントロールは、SharePoint サンドボックス環境でサポートされていません。 サンドボックス ソリューションの視覚的 web パーツでサポート対象外のコントロールを使用すると、"型または名前空間の名前 'Theme' は名前空間 'Microsoft.SharePoint.WebControls' に存在しません" というエラーが表示されます。

  サンドボックスソリューションの詳細については、「[サンドボックスソリューションとファームソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)」を参照してください。

## <a name="create-older-style-sharepoint-based-web-parts"></a>旧形式の SharePoint ベースの web パーツを作成する
 Visual Studio のテンプレートを使用すると、SharePoint 用の独自の [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web パーツを作成できます。 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web パーツは [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] Web パーツのインフラストラクチャ上にビルドされるので、新しいプロジェクトに適しています。

 ごくまれに、古い形式の SharePoint に対応する Web パーツを使用して Web パーツを作成しなければならない場合があります。 こうした Web パーツも Visual Studio で作成できますが、Visual Studio にはその際に役立つテンプレートがありません。

 旧形式の SharePoint ベースの web パーツを作成する場合の詳細については、「 [Windows Sharepoint Services の Web パーツインフラストラクチャ](/previous-versions/office/developer/sharepoint-2010/ms415560(v=office.14))」を参照してください。 旧形式の SharePoint ベースの web パーツを使用して web パーツを作成する方法の詳細については、「[チュートリアル: 基本的な Sharepoint Web パーツを作成](/previous-versions/office/ms452873(v=office.14))する」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|[説明]|
|-----------|-----------------|
|[方法: SharePoint web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)|SharePoint ページの Web パーツを作成する方法について説明します。|
|[方法: デザイナーを使用して SharePoint web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|視覚的なデザイン サーフェイスを使用して、SharePoint の Web パーツを作成する方法について説明します。|
|[方法: SharePoint アプリケーションページまたは web パーツのユーザーコントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|SharePoint で実行されるアプリケーション ページと Web パーツで使用できる、再利用可能なカスタム コントロールを作成する方法について説明します。|
|[チュートリアル: SharePoint の web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|SharePoint の Web パーツをデザインする方法について説明します。|
|[チュートリアル: デザイナーを使用した SharePoint の web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|視覚的なデザイン サーフェイスにコントロールをドラッグして、SharePoint の Web パーツをデザインする方法について説明します。|
|[チュートリアル: SharePoint の OData を表示する Silverlight web パーツの作成](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|Silverlight アプリケーションをホストし、SharePoint リストのデータを表示する、SharePoint の Web パーツをデザインする方法について説明します。|
