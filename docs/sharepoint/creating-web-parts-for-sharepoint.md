---
title: SharePoint の Web パーツを作成する | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015052"
---
# <a name="create-web-parts-for-sharepoint"></a>SharePoint の Web パーツを作成する
  Web パーツを作成すると、SharePoint サイト ページのコンテンツ、外観、および動作をユーザーがブラウザーから変更できます。 Web パーツは、Web パーツ ページ内で実行されるサーバー側コントロールです。SharePoint サイトに表示されるページはこれらの Web パーツで構成されます。 「[構成要素: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

 SharePoint サイトの Web パーツを作成およびデバッグするには、Visual Studio のテンプレートを使用します。

## <a name="create-a-web-part-in-visual-studio"></a>Visual Studio で Web パーツを作成する
 Web パーツを作成するには、SharePoint プロジェクトに **Web パーツ**項目を追加します。 サンドボックス ソリューションまたはファーム ソリューションに **Web パーツ**項目を使用できます。

 デザイナーを使用して Web パーツを視覚的にデザインする場合は、**視覚的 Web パーツ** プロジェクトを作成するか、**視覚的 Web パーツ**項目を SharePoint プロジェクトに追加します。 **視覚的 Web パーツ**項目を使用できるのは、ファーム ソリューションのみです。

### <a name="web-part-item"></a>Web パーツ項目
 **Web パーツ**項目には、SharePoint サイト用の Web パーツをデザインするためのファイルが用意されています。 **Web パーツ**項目を追加すると、プロジェクトにフォルダーが作成され、そのフォルダーにいくつかのファイルが追加されます。 各ファイルの説明を次の表に示します。

|ファイル|説明|
|----------|-----------------|
|*Elements.xml*|Web パーツを配置する際、プロジェクトのフィーチャー定義ファイルで使用する情報が格納されます。|
|.webpart ファイル|SharePoint の Web パーツ ギャラリーに Web パーツを表示するために必要な情報を指定します。|
|コード ファイル|Web パーツにコントロールを追加するメソッド、および Web パーツ内にカスタム コンテンツを生成するメソッドが保存されます。|

 詳細については、「[方法:SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)」を参照してください。

### <a name="visual-web-part-item"></a>視覚的 Web パーツ項目
 視覚的 Web パーツは、Visual Studio の Visual Web Developer デザイナーを使用して作成する Web パーツです。 視覚的 Web パーツの機能は他の Web パーツと同じです。 ボタンやテキスト ボックスなどのコントロールを Web パーツに追加するときは、XML ファイルにコードを追加します。 ただし、視覚的 Web パーツにコントロールを追加するときは、Visual Studio の**ツールボックス**から Web パーツへコントロールをドラッグまたはコピーします。 その後、XML ファイルで必要なコードを生成します。 「[方法:デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)」を参照してください。

## <a name="sharepoint-controls"></a>SharePoint コントロール
 Visual Studio には、アプリケーションのページなど、SharePoint ページを作成するためのコントロールが用意されています。 これらのコントロールは、**ツールボックス**の **[SharePoint コントロール]** の下に表示されます。 これらのコントロールの機能は、[Microsoft.SharePoint.WebControls](/previous-versions/office/sharepoint-server/ms413880(v=office.15)) 名前空間から取得されます。ここには、SharePoint のサイトやリストのページで使用する ASP.NET サーバー コントロールが含まれています。

|コントロール名|説明|
|------------------|-----------------|
|[AspMenu](/previous-versions/office/sharepoint-server/ms454108(v=office.15))|ASP メニューを挿入します。 詳細については、「[メニュー コントロールの概要](/previous-versions/ecs0x9w5(v=vs.140))」を参照してください。|
|[CssLink](/previous-versions/office/sharepoint-server/ms439048(v=office.15))|**LINK** 要素を *.aspx* ページに挿入し、**CssRegistration**で定義されている外部スタイル シートを適用します。|
|[DateTimeControl](/previous-versions/office/sharepoint-server/ms414993(v=office.15))|*.aspx* ページに DateTime コントロールを挿入します。|
|[FormDigest](/previous-versions/office/sharepoint-server/ms416616(v=office.15))|*.aspx* ページにセキュリティ検証を挿入します|
|[ListProperty](/previous-versions/office/sharepoint-server/ms455032(v=office.15))|指定されたリストのプロパティを返します。|
|[ProjectProperty](/previous-versions/office/sharepoint-server/ms478990(v=office.15))|現在の Web サイトのグローバル プロパティを返します。|
|[RssLink](/previous-versions/office/sharepoint-server/ms457574(v=office.15))|RSS フィードへのリンクを *.aspx* ページに挿入します。|
|[ScriptLink](/previous-versions/office/sharepoint-server/ms411959(v=office.15))|スクリプトなどのリソースをページに登録し、ページのレンダリング時に要求できるようにするためのプロパティとメソッドを提供します。|
|[テーマ](/previous-versions/office/sharepoint-server/ms460735(v=office.15))|*.aspx* ページにテーマを適用します。|

## <a name="debug-a-web-part"></a>Web パーツをデバッグする
 他の Visual Studio プロジェクトをデバッグする場合と同様に、Web パーツを含む SharePoint プロジェクトをデバッグできます。 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 コードのデバッグを開始するには、SharePoint で Web パーツ ページに Web パーツを追加します。

 SharePoint プロジェクトのデバッグ方法の詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="visual-web-part-limitations"></a>視覚的 Web パーツの制限
 Visual Studio では、SharePoint のサンドボックス ソリューションおよびファーム ソリューションに視覚的 Web パーツを追加できます。 ただし、視覚的 Web パーツには次のような制限があります。

- 視覚的 Web パーツでは置き換え可能パラメーターを使用できません。 詳細については、「[置き換え可能パラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

- ユーザー コントロールと視覚的 Web パーツは、視覚的 Web パーツ上にドラッグ アンド ドロップしたり、コピーしたりできません。 これらの操作を実行するとビルド エラーが発生します。

- 視覚的 Web パーツは、$SPUrl などの SharePoint サーバー トークンを直接サポートしません。 詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」トピックの「サンドボックス視覚的 Web パーツでのトークンの制約」を参照してください。

- サンドボックス ソリューションの視覚的 Web パーツは、"Sandboxed Code Host Service がビジー状態で要求を処理できなかったので、セキュリティで保護されたコード実行要求が拒否されました" というエラーが発生する場合があります。 このエラーの詳細については、[SharePoint 開発者チーム ブログ](https://blogs.msdn.microsoft.com/sharepointdev/2011/02/08/error-the-sandboxed-code-execution-request-was-refused-because-the-sandboxed-code-host-service-was-too-busy-to-handle-the-request-ricky-kirkham/#10149157)の投稿を参照してください。

- Visual Studio では、サーバー側 JavaScript のデバッグがサポートされていません。ただし、クライアント側 JavaScript のデバッグはサポートされています。

   サーバー側のマークアップ ファイルにインライン JavaScript を追加できますが、マークアップに追加したブレークポイントはデバッグできません。 JavaScript をデバッグするには、マークアップ ファイルで外部の JavaScript ファイルを参照し、JavaScript ファイルにブレークポイントを設定します。

- インライン [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] コードのデバッグは、マークアップ ファイルではなく、生成されたコード ファイルで実行する必要があります。

- 視覚的 Web パーツでは、`<@ Assembly Src=` ディレクティブを使用できません。

- SharePoint の Web コントロールと一部の [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] コントロールは、SharePoint サンドボックス環境でサポートされていません。 サンドボックス ソリューションの視覚的 web パーツでサポート対象外のコントロールを使用すると、"型または名前空間の名前 'Theme' は名前空間 'Microsoft.SharePoint.WebControls' に存在しません" というエラーが表示されます。

  サンドボックス ソリューションの詳細については、「[サンドボックス ソリューションとファーム ソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)」を参照してください。

## <a name="create-older-style-sharepoint-based-web-parts"></a>古い形式の SharePoint に基づく Web パーツを作成する
 Visual Studio のテンプレートを使用すると、SharePoint 用の独自の [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web パーツを作成できます。 [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web パーツは [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] Web パーツのインフラストラクチャ上にビルドされるので、新しいプロジェクトに適しています。

 ごくまれに、古い形式の SharePoint に対応する Web パーツを使用して Web パーツを作成しなければならない場合があります。 こうした Web パーツも Visual Studio で作成できますが、Visual Studio にはその際に役立つテンプレートがありません。

 古い形式の SharePoint に対応する Web パーツを作成するケースについては、[Windows SharePoint Services の Web パーツ インフラストラクチャ](/previous-versions/office/developer/sharepoint-2010/ms415560(v=office.14))に関するページを参照してください。 古い形式の SharePoint に基づく Web パーツを使用して Web パーツを作成する方法については、「[チュートリアル: 基本的な SharePoint Web パーツの作成](/previous-versions/office/ms452873(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)|SharePoint ページの Web パーツを作成する方法について説明します。|
|[方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|視覚的なデザイン サーフェイスを使用して、SharePoint の Web パーツを作成する方法について説明します。|
|[方法: SharePoint アプリケーション ページまたは Web パーツのユーザー コントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|SharePoint で実行されるアプリケーション ページと Web パーツで使用できる、再利用可能なカスタム コントロールを作成する方法について説明します。|
|[チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|SharePoint の Web パーツをデザインする方法について説明します。|
|[チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|視覚的なデザイン サーフェイスにコントロールをドラッグして、SharePoint の Web パーツをデザインする方法について説明します。|
|[チュートリアル: SharePoint の OData を表示する Silverlight Web パーツの作成](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|Silverlight アプリケーションをホストし、SharePoint リストのデータを表示する、SharePoint の Web パーツをデザインする方法について説明します。|
