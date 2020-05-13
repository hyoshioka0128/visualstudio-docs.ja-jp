---
title: プロジェクトテンプレートとプロジェクト項目テンプレート |マイクロソフトドキュメント
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.FirstWizardPage
- VS.SharePointTools.SPE.ListInstance
- VS.SharePointTools.SPE.ListDefinition
- VS.SharePointTools.SPE.ListDefFromContentType
- VS.SharePointTools.SPE.ContentType
- SPE.Wizard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, project and project item templates
- SharePoint development in Visual Studio, templates
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2878bd2092e000cf63c2b4fcb531a502a470203e
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649223"
---
# <a name="sharepoint-project-and-project-item-templates"></a>プロジェクトテンプレートとプロジェクト項目テンプレート
  以下のセクションでは、SharePoint プロジェクトとプロジェクト項目の使用可能なテンプレート、およびそれらの使用方法について説明します。

## <a name="project-and-project-item-templates-overview"></a>プロジェクトおよびプロジェクト項目テンプレートの概要
 Visual Studio で新しい SharePoint プロジェクトを作成すると、その種類のプロジェクトに必要なすべてのプロジェクト項目と共にソリューションに追加されます。 たとえば、Silverlight Web パーツ プロジェクトを作成した場合、視覚的 Web パーツ プロジェクト項目と Silverlight アプリケーション プロジェクト項目、およびそれらのプロジェクト項目に必要なすべてのファイルを含むソリューションが作成されます。 プロジェクト項目テンプレートは、既存の SharePoint プロジェクトにプロジェクト項目 (イベント レシーバー、サイト列、リストなど) を追加する目的で使用されます。

 SharePoint の基本事項の詳細については[、「SharePoint ファウンデーションの構成要素](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))」を参照してください。 上級ユーザーは、プロジェクトやプロジェクト項目のテンプレートを独自に作成することもできます。 詳細については、「 [SharePoint プロジェクト システムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

## <a name="project-templates"></a>プロジェクト テンプレート
 ここでは、それぞれの SharePoint プロジェクト テンプレートについて説明します。 Visual Studio で SharePoint プロジェクト テンプレートを表示するには、[**新しいプロジェクト**] ダイアログ ボックスで **、[Visual C#]** または **[Visual Basic]** の下の **[SharePoint]** ノードを展開し **、[2010]** を選択します。

### <a name="sharepoint-2010-project"></a>プロジェクト
 *SharePoint 2010 プロジェクト*の内容は、すべての SharePoint プロジェクト テンプレートに含まれています。 SharePoint 2010 プロジェクトの内容は次のとおりです。

- プロジェクト ファイル。

- プロジェクトのプロパティ ページ。

- プロジェクト内のすべてのアセンブリ参照を一覧表示する**参照**フォルダ。

- **SharePoint**サーバーに機能を展開するために使用される *.feature*構成ファイルを含むフィーチャー フォルダー。

- ソリューションを SharePoint に展開するために使用される*Package.package*ファイルを含む**パッケージ**フォルダー。

- key.snk (厳密名キー) ファイル。セキュリティ対策としてアセンブリに厳密な名前で署名するために使用されます。

### <a name="sharepoint-2010-silverlight-web-part"></a>2010 年のシルバーライト Web パーツ
 *SharePoint 2010 の Web パーツ*プロジェクトを使用すると、Silverlight アプリケーションを表示する SharePoint 用の Web パーツを作成できます。 このプロジェクトを作成するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを参照するかを指定できます。 詳細については、「 [SharePoint の Web パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md)」および[「チュートリアル: SharePoint の OData を表示する Silverlight Web パーツを作成する](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)」を参照してください。

### <a name="sharepoint-2010-visual-web-part"></a>ビジュアル Web パーツ
 *SharePoint 2010 ビジュアル Web パーツ*プロジェクトには *、Elements.xml*定義ファイル **、Web パーツ**アイテム、およびユーザー**コントロール**アイテムが含まれています。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「 [[方法] デザイナーと構成要素を使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) [: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="import-sharepoint-2010-solution-package"></a>SharePoint 2010 ソリューション パッケージのインポート
 *SharePoint 2010 ソリューション パッケージ*のインポート プロジェクトを使用すると、既存の SharePoint 2010 サイトの全体 *.wsp*または一部をインポートできます。 Visual Studio にインポートした後は、その項目をカスタマイズして再配置することができます。 詳細については、「[既存の SharePoint サイトからアイテムをインポートする](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

### <a name="import-reusable-sharepoint-2010-workflow"></a>再利用可能な SharePoint 2010 ワークフローをインポートする
 *再利用可能な SharePoint 2010 ワークフロー*プロジェクトをインポートすると、SharePoint デザイナー 2010 で作成された再利用可能な宣言型ワークフローを Visual Studio にインポートできます。 ワークフローは、SharePoint サイトから *.wsp*ファイルとしてエクスポートされます。 Visual Studio にインポートした後は、カスタマイズしたりコードを追加したりして、SharePoint サイトに配置できます。 詳細については、「[チュートリアル: SharePoint デザイナーの再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)」を参照してください。

## <a name="project-item-templates"></a>プロジェクト項目テンプレート
 ここでは、それぞれの SharePoint プロジェクト項目テンプレートについて説明します。 プロジェクト項目テンプレートでは、サイト列、リスト、コンテンツ タイプなどの SharePoint 機能をサポートするために、SharePoint ソリューションにファイルを追加します。 たとえば、サイト列をソリューションに追加すると *、Elements.xml*定義ファイルを含むサイト列プロジェクトが追加されます。 ビジュアル Web パーツを追加すると *、Elements.xml*ファイル、ユーザー コントロール項目、およびビジュアル Web パーツ項目を含むビジュアル Web パーツ プロジェクトがソリューションに追加されます。

 SharePoint プロジェクト項目テンプレートを表示するには、**ソリューション エクスプローラー**で SharePoint プロジェクトのショートカット メニューを開き、[**追加**]、[**新しい項目**] の順にクリックします。 [Visual **C#]** または **[Visual Basic]** の下の **[SharePoint]** ノードを展開し **、[2010]** を選択します。

### <a name="application-page-farm-solution-only"></a>アプリケーション ページ (ファーム ソリューションのみ)
 **アプリケーション ページ (ファーム ソリューションのみ)** 項目を使用[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]すると、SharePoint サイトの Web ページをデザインできます。 アプリケーション ページは、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[方法 : アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)」および「 アプリケーション _layouts[ページの種類](/previous-versions/office/aa979604(v=office.14))」を参照してください。

### <a name="business-data-connectivity-model-farm-solution-only"></a>ビジネス データ接続モデル (ファーム ソリューションのみ)
 **ビジネス データ接続モデル (ファーム ソリューションのみ)** 項目を使用すると、ビジネス データを SharePoint に統合できます。 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]、Siebel、Service Advertising Protocol (SAP) などのバック エンドのサーバー アプリケーションからのデータを使用できます。 ビジネス データ接続モデル (ファーム ソリューションのみ) は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[方法 : BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)、[方法 : リソース ファイルを使用してローカライズされた名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)」、および[「新機能 : ビジネス接続サービス](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))」を参照してください。

### <a name="content-type"></a>Content type
 *コンテンツ タイプ*アイテムを使用すると、ドキュメント、お知らせ、タスクなどの既存の (ベース) コンテンツ タイプに基づいてカスタム コンテンツ タイプを作成できます。 カスタム コンテンツ タイプでは、独自に定義したサイト列 (フィールド) に加えて、ベース コンテンツ タイプと同じ属性およびフィールドを使用できます。 たとえば、SharePoint に付属している基本の Contact コンテンツ タイプを基にしてカスタムの Contact コンテンツ タイプを作成できます。 コンテンツ タイプのカスタマイズでは、基本コンテンツ タイプの既存のサイト列を変更したり、別のサイト列を追加したりできます。

> [!NOTE]
> SharePoint の制限により、サンドボックス ソリューション コンテンツ タイプを基にしてファーム ソリューション コンテンツ タイプを作成することはできません。

 詳細については、「[チュートリアル: SharePoint および構成要素のサイト列、コンテンツ タイプ、およびリストを作成する](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) [: コンテンツ タイプ](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))」を参照してください。

### <a name="empty-element"></a>空要素
 *空の要素*は、Visual Studio でプロジェクトまたはプロジェクト項目テンプレートを持たない SharePoint プロジェクト項目を定義するために最もよく使用されます。 空の要素をプロジェクトに追加すると、EmptyElement[x] という名前のノードが作成されます(ここで[x]\)は一意の番号です)。 空要素 [x] には *、Elements.xml*という名前の単一のファイルが含まれています。 ステートメント[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]を使用して *、Elements.xml*で目的の要素を定義します。

### <a name="event-receiver"></a>イベント レシーバー
 *イベント レシーバーは*、リストにアイテムが追加されたとき、Web アイテムが削除されたとき、ワークフローが開始されたときなど、SharePoint サイト内のアイテムのイベントを処理します。 イベント レシーバー プロジェクト項目テンプレートで処理できるイベントは次のとおりです。

- イベントを一覧表示します

- リスト アイテム イベント

- リスト電子メール イベント

- Web イベント

- リスト ワークフロー イベント

  イベント レシーバー プロジェクト項目は **、SharePoint カスタマイズ ウィザード**でプロジェクトを作成したときに指定したすべてのイベントのイベント ハンドラーを含む単一のクラス ファイルを持つ**イベント レシーバー**フォルダーを作成します。 イベント レシーバー クラスは、ファイル、フィールド、アイテム、リスト、添付ファイル、Web パーツ、ワークフローなどのアイテムが追加、更新、削除、または削除されたときに SharePoint サイトで発生するイベントを処理できます。 詳細については、「方法[: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)」および「[構成要素: イベント処理」](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))を参照してください。

### <a name="list"></a>List
 リストは、再利用可能な基本の SharePoint リスト定義のインスタンスです (予定表、タスク リストなど)。 ソリューションにリストを追加した後、リスト デザイナーで、リストにサイト列を追加したり、リストのカスタム列を作成したりできます。 これにはコンテンツ タイプのサイト列が含まれます。 リストに表示する列を決定する*リストのビュー*を指定できます。 詳細については、「[チュートリアル: SharePoint および文書パーツブロックのサイト列、コンテンツ タイプ、およびリストを作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)する[: リストとドキュメント ライブラリ](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))」を参照してください。

### <a name="module"></a>Module
 *モジュール*(モジュールと[!include[vbprvb](../sharepoint/includes/vbprvb-md.md)]混同しないように) には、イメージやメモなど、SharePoint サーバーに展開するファイルが含まれます。 モジュール プロジェクト項目には **、モジュール**ノードが含まれています。 モジュール ノードには、モジュールのマニフェストとして機能する XML 定義ファイルと、placeholder ファイルの*sample.txt*ファイルという 2 つのプロジェクト項目テンプレートが含まれます。 詳細については、「[モジュールを使用してソリューションおよびモジュールにファイルをインクルードする](../sharepoint/using-modules-to-include-files-in-the-solution.md) [」を参照してください](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))。

### <a name="sequential-workflow-farm-solution-only"></a>シーケンシャル ワークフロー (ファーム ソリューションのみ)
 *シーケンシャル ワークフロー*は、最後のステップが完了するまで順番に実行される一連のビジネス ロジック ステップです。 シーケンシャル ワークフローは、リストやドキュメントなどの SharePoint アイテムが関係するプロセスを管理する目的で使用します。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できるほか、ワークフローを自動的に開始するか、手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、SharePoint [Server 2010 のワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))、および[新機能 : ワークフローの改善](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))」を参照してください。

### <a name="silverlight-web-part"></a>シルバーライト Web パーツ
 *Web パーツ*プロジェクト項目を使用すると、Silverlight アプリケーションを表示する SharePoint 用の Web パーツを作成できます。 このプロジェクト項目ソリューションに追加するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを後で参照するかを選択できます。 詳細については、「 [SharePoint の Web パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md)」および[「チュートリアル: SharePoint の OData を表示する Silverlight Web パーツを作成する](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)」を参照してください。

### <a name="site-column"></a>サイト列
 *サイト列*( フィールドとも呼ばれます *)* は、SharePoint プロジェクトに追加できる最も基本的な要素の 1 つです。 サイト列はデータの種類を表します。たとえば、連絡先一覧であれば、連絡先の電話番号、テキスト コメント、都市名などです。 詳細については、「 [SharePoint および列のサイト列、コンテンツ タイプ、およびリストを作成する](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)」を[参照してください](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

### <a name="site-definition-farm-solution-only"></a>サイト定義 (ファーム ソリューションのみ)
 *サイト定義*プロジェクトアイテムには、次のファイルを含むサイト定義フォルダが含まれています。

- 既定の .aspx ページ。サイトの既定の Web ページとして使用されます。

- サイトのコンポーネントを定義する*onet.xml*ファイル。

- **[新しい SharePoint**サイト] ページの **[テンプレートの選択]** セクションに表示されるサイト定義構成を指定する webtemp xml ファイル。

  サイト定義の追加後は、コードおよびファイルを追加して機能を導入できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [SharePoint のサイト定義とサイト定義](../sharepoint/creating-site-definitions-for-sharepoint.md)[と構成](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))の作成 」を参照してください。

### <a name="state-machine-workflow-farm-solution-only"></a>ステート マシン のワークフロー (ファーム ソリューションのみ)
 *ステート マシン ワークフロー*は、ビジネス ロジックの状態、遷移、およびアクションのセットです。 ステート マシン ワークフローに含まれる各ステップは、順番に実行されるのではなく、アクションおよび状態によってトリガーされます。 シーケンシャル ワークフローと同様に、ステート マシン ワークフローは、リストやドキュメントなどの SharePoint アイテムに関連付けられます。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できることも、シーケンシャル ワークフローと同じです。 ワークフローを自動的に開始するか手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、SharePoint [Server 2010 のワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))、および[新機能 : ワークフローの改善](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))」を参照してください。

### <a name="user-control-farm-solution-only"></a>ユーザーコントロール (ファーム ソリューションのみ)
 *ユーザー コントロール*は、他のASP.NET コントロールおよび SharePoint コントロールを追加できる、再利用可能なカスタム コントロールです。 ユーザー コントロールは、SharePoint で実行されるアプリケーション ページと Web パーツに追加できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [Web パーツまたはアプリケーション ページ用の再利用可能なコントロールの作成](creating-reusable-controls-for-web-parts-or-application-pages.md)」を参照してください。

### <a name="visual-web-part"></a>ビジュアル Web パーツ
 *視覚的 Web パーツ*プロジェクト項目には *、Elements.xml*定義ファイル **、Web パーツ**項目、およびユーザー**コントロール**項目が含まれます。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「 [[方法] デザイナーと構成要素を使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) [: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="web-part"></a>Web パーツ
 *Web パーツ*は、Web パーツ ページと呼ばれる特殊な種類のページ内で実行されるサーバー側コントロールです。 これらは、SharePoint サイトに表示されるページのビルド ブロックです。 Web パーツ項目には、SharePoint サイト用の Web パーツをデザインするためのファイルが用意されています。 詳細については、「[方法 : SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)」および「[構成要素 : Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint 製品とテクノロジ](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))
