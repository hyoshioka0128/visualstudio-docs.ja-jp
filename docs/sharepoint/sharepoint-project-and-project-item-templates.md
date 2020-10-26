---
title: SharePoint プロジェクトとプロジェクト項目テンプレート |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "81649223"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint プロジェクトとプロジェクト項目テンプレート
  以下のセクションでは、SharePoint プロジェクトとプロジェクト項目の使用可能なテンプレート、およびそれらの使用方法について説明します。

## <a name="project-and-project-item-templates-overview"></a>プロジェクトとプロジェクト項目テンプレートの概要
 Visual Studio で新しい SharePoint プロジェクトを作成すると、その種類のプロジェクトに必要なすべてのプロジェクト項目と共にソリューションに追加されます。 たとえば、Silverlight Web パーツ プロジェクトを作成した場合、視覚的 Web パーツ プロジェクト項目と Silverlight アプリケーション プロジェクト項目、およびそれらのプロジェクト項目に必要なすべてのファイルを含むソリューションが作成されます。 プロジェクト項目テンプレートは、既存の SharePoint プロジェクトにプロジェクト項目 (イベント レシーバー、サイト列、リストなど) を追加する目的で使用されます。

 SharePoint の基礎の詳細については、「 [Sharepoint Foundation の構成要素](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))」を参照してください。 上級ユーザーは、プロジェクトやプロジェクト項目のテンプレートを独自に作成することもできます。 詳細については、「 [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

## <a name="project-templates"></a>プロジェクト テンプレート
 ここでは、それぞれの SharePoint プロジェクト テンプレートについて説明します。 Visual Studio で SharePoint プロジェクトテンプレートを表示するには、[**新しいプロジェクト**] ダイアログボックスで、[ **visual C#** ] または [ **Visual Basic**] の下にある [ **sharepoint** ] ノードを展開し、[ **2010**] を選択します。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 プロジェクト
 *Sharepoint 2010 プロジェクト*の内容は、すべての sharepoint プロジェクトテンプレートに含まれています。 SharePoint 2010 プロジェクトの内容は次のとおりです。

- プロジェクト ファイル。

- プロジェクトのプロパティ ページ。

- プロジェクト内のすべてのアセンブリ参照を一覧表示する **参照** フォルダー。

- 機能の構成ファイルを含む **features** フォルダー *。* SharePoint サーバーにフィーチャーを配置するために使用されます。

- ソリューションを SharePoint に配置するために使用さ*れるパッケージパッケージファイルを*含む**パッケージ**フォルダー。

- key.snk (厳密名キー) ファイル。セキュリティ対策としてアセンブリに厳密な名前で署名するために使用されます。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight web パーツ
 *Sharepoint 2010 Silverlight Web パーツ* プロジェクトを使用すると、silverlight アプリケーションを表示する sharepoint の web パーツを作成できます。 このプロジェクトを作成するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを参照するかを指定できます。 詳細については、「 [sharepoint の web パーツを作成](../sharepoint/creating-web-parts-for-sharepoint.md) する」および「 [チュートリアル: sharepoint の OData を表示する Silverlight Web パーツを作成](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)する」を参照してください。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 視覚的 web パーツ
 *SharePoint 2010 の視覚的 Web パーツ*プロジェクトには *、Elements.xml*定義ファイル、 **Web パーツ**項目、および**ユーザーコントロール**項目が含まれています。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「方法: デザイナーとビルドブロックを [使用して SharePoint web パーツを作成](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) する [: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="import-sharepoint-2010-solution-package"></a>SharePoint 2010 ソリューションパッケージのインポート
 *Sharepoint 2010 ソリューションパッケージ* プロジェクトをインポートすると、sharepoint ソリューション (*.wsp*) ファイルにエクスポートされた既存の sharepoint 2010 サイトのすべてまたは一部を Visual Studio にインポートできます。 Visual Studio にインポートした後は、その項目をカスタマイズして再配置することができます。 詳細については、「 [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

### <a name="import-reusable-sharepoint-2010-workflow"></a>再利用可能な SharePoint 2010 ワークフローのインポート
 *再利用可能な sharepoint 2010 ワークフロー* プロジェクトをインポートすると、sharepoint Designer 2010 で作成した再利用可能な宣言型のワークフローを Visual Studio にインポートできます。 ワークフローは、SharePoint サイトから *.wsp* ファイルとしてエクスポートされます。 Visual Studio にインポートした後は、カスタマイズしたりコードを追加したりして、SharePoint サイトに配置できます。 詳細については、「 [チュートリアル: SharePoint Designer の再利用可能なワークフローの Visual Studio へのインポート](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)」を参照してください。

## <a name="project-item-templates"></a>プロジェクト項目テンプレート
 ここでは、それぞれの SharePoint プロジェクト項目テンプレートについて説明します。 プロジェクト項目テンプレートでは、サイト列、リスト、コンテンツ タイプなどの SharePoint 機能をサポートするために、SharePoint ソリューションにファイルを追加します。 たとえば、ソリューションにサイト列を追加すると、 *Elements.xml* 定義ファイルを含むサイト列プロジェクトが追加されます。 視覚的 web パーツを追加すると、 *Elements.xml* ファイル、ユーザーコントロール項目、および視覚的な web パーツ項目を含むビジュアル web パーツプロジェクトがソリューションに追加されます。

 SharePoint プロジェクト項目テンプレートを表示するには、 **ソリューションエクスプローラー**で、sharepoint プロジェクトのショートカットメニューを開き、[ **追加**]、[ **新しい項目**] の順に選択します。 [ **Visual C#** ] または [ **Visual Basic**] の [ **SharePoint** ] ノードを展開し、[ **2010**] を選択します。

### <a name="application-page-farm-solution-only"></a>[アプリケーション] ページ (ファームソリューションのみ)
 **アプリケーションページ (ファームソリューションのみ)** 項目を使用すると、 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] SharePoint サイトの web ページをデザインできます。 アプリケーション ページは、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [方法: アプリケーションページ](../sharepoint/how-to-create-an-application-page.md) と [アプリケーション _Layouts ページの種類](/previous-versions/office/aa979604(v=office.14))を作成する」を参照してください。

### <a name="business-data-connectivity-model-farm-solution-only"></a>ビジネスデータ接続モデル (ファームソリューションのみ)
 **ビジネスデータ接続モデル (ファームソリューションのみ)** 項目を使用すると、ビジネスデータを SharePoint に統合できます。 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]、Siebel、Service Advertising Protocol (SAP) などのバック エンドのサーバー アプリケーションからのデータを使用できます。 ビジネス データ接続モデル (ファーム ソリューションのみ) は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [方法: BDC モデルを作成](../sharepoint/how-to-create-a-bdc-model.md)する」、「 [方法: リソースファイルを使用してローカライズされた名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)」、および「 [新機能: Business Connectivity Services](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))」を参照してください。

### <a name="content-type"></a>Content type
 *コンテンツタイプ* 項目を使用すると、ドキュメント、アナウンス、タスクなどの既存の (基本) コンテンツタイプに基づいて、カスタムコンテンツタイプを作成できます。 カスタム コンテンツ タイプでは、独自に定義したサイト列 (フィールド) に加えて、ベース コンテンツ タイプと同じ属性およびフィールドを使用できます。 たとえば、SharePoint に付属している基本の Contact コンテンツ タイプを基にしてカスタムの Contact コンテンツ タイプを作成できます。 コンテンツ タイプのカスタマイズでは、基本コンテンツ タイプの既存のサイト列を変更したり、別のサイト列を追加したりできます。

> [!NOTE]
> SharePoint の制限により、サンドボックス ソリューション コンテンツ タイプを基にしてファーム ソリューション コンテンツ タイプを作成することはできません。

 詳細については、「 [チュートリアル: サイト列、コンテンツタイプ、および SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) と [構成要素](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))のリストの作成」を参照してください。

### <a name="empty-element"></a>空要素
 *空の要素* は、Visual Studio でプロジェクトまたはプロジェクト項目テンプレートがない SharePoint プロジェクト項目を定義するために最もよく使用されます。 プロジェクトに空の要素を追加すると、EmptyElement [x] という名前のノードが作成されます (ここで [x] は一意の番号です) \) 。 EmptyElement [x] には、Elements.xml という名前の1つのファイルが含まれてい * ます。* [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]ステートメントを使用して、 *Elements.xml*に必要な要素を定義します。

### <a name="event-receiver"></a>イベントレシーバー
 *イベントレシーバー* は、項目がリストに追加されたとき、web 項目が削除されたとき、またはワークフローが開始されたときなど、SharePoint サイト内の項目のイベントを処理します。 イベント レシーバー プロジェクト項目テンプレートで処理できるイベントは次のとおりです。

- イベントを一覧表示します

- リスト アイテム イベント

- リスト電子メール イベント

- Web イベント

- リスト ワークフロー イベント

  イベントレシーバープロジェクト項目では、 **SharePoint カスタマイズウィザード**でプロジェクトを作成したときに指定したすべてのイベントのイベントハンドラーを含む、単一のクラスファイルを持つ**イベントレシーバー**フォルダーが作成されます。 イベントレシーバークラスは、ファイル、フィールド、項目、リスト、添付ファイル、web パーツ、ワークフローなどの項目が追加、更新、削除、または削除されたときに、SharePoint サイトで発生するイベントを処理できます。 詳細については、「 [方法: イベントレシーバーを作成](../sharepoint/how-to-create-an-event-receiver.md) する」および「 [構成要素: イベント処理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))」を参照してください。

### <a name="list"></a>リスト
 リストは、再利用可能な基本の SharePoint リスト定義のインスタンスです (予定表、タスク リストなど)。 ソリューションにリストを追加した後、リスト デザイナーで、リストにサイト列を追加したり、リストのカスタム列を作成したりできます。 これにはコンテンツ タイプのサイト列が含まれます。 一覧に表示される列を決定する *ビュー* を指定できます。 詳細については、「 [チュートリアル: サイト列、コンテンツタイプ、および SharePoint のリスト](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) と [ドキュメントライブラリ](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))の作成」を参照してください。

### <a name="module"></a>モジュール
 *モジュール* (モジュールと混同しないで [!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] ください) には、SharePoint サーバーに配置するファイル (画像やメモなど) が含まれています。 モジュールプロジェクトアイテムに **モジュール** ノードが含まれています。 モジュールノードには、モジュールのマニフェストとして機能する XML 定義ファイルと、 *sample.txt* ファイル (プレースホルダーファイル) という2つのプロジェクト項目テンプレートが含まれています。 詳細については、「モジュールを使用してソリューションと[モジュール](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))[にファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)」を参照してください。

### <a name="sequential-workflow-farm-solution-only"></a>シーケンシャルワークフロー (ファームソリューションのみ)
 *シーケンシャルワークフロー*は、最後のステップが完了するまで順番に実行される一連のビジネスロジックステップです。 シーケンシャル ワークフローは、リストやドキュメントなどの SharePoint アイテムが関係するプロセスを管理する目的で使用します。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できるほか、ワークフローを自動的に開始するか、手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [sharepoint ワークフローソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、「 [sharepoint Server 2010 のワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))」、および「 [新機能: ワークフローの機能強化](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))」を参照してください。

### <a name="silverlight-web-part"></a>Silverlight web パーツ
 *Silverlight web パーツ* プロジェクト項目を使用すると、silverlight アプリケーションを表示する SharePoint の web パーツを作成できます。 このプロジェクト項目ソリューションに追加するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを後で参照するかを選択できます。 詳細については、「 [sharepoint の web パーツを作成](../sharepoint/creating-web-parts-for-sharepoint.md) する」および「 [チュートリアル: sharepoint の OData を表示する Silverlight Web パーツを作成](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)する」を参照してください。

### <a name="site-column"></a>サイト列
 *サイト列*は、*フィールド*とも呼ばれ、SharePoint プロジェクトに追加できる最も基本的な要素の1つです。 サイト列はデータの種類を表します。たとえば、連絡先一覧であれば、連絡先の電話番号、テキスト コメント、都市名などです。 詳細については、「SharePoint および[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))[のサイト列、コンテンツタイプ、およびリストを作成する](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)」を参照してください。

### <a name="site-definition-farm-solution-only"></a>サイト定義 (ファームソリューションのみ)
 *サイト定義* プロジェクトアイテムには、次のファイルを含むサイト定義フォルダーが含まれています。

- 既定の .aspx ページ。サイトの既定の Web ページとして使用されます。

- サイトのコンポーネントを定義する *onet.xml* ファイル。

- [**新しい SharePoint サイト**] ページの [**テンプレートの選択**] セクションに表示されるサイト定義の構成を指定する webtemp xml ファイルです。

  サイト定義の追加後は、コードおよびファイルを追加して機能を導入できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「SharePoint および[サイト定義と構成](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))[のサイト定義の作成](../sharepoint/creating-site-definitions-for-sharepoint.md)」を参照してください。

### <a name="state-machine-workflow-farm-solution-only"></a>ステートマシンのワークフロー (ファームソリューションのみ)
 *ステートマシンワークフロー*は、ビジネスロジックの状態、遷移、およびアクションのセットです。 ステート マシン ワークフローに含まれる各ステップは、順番に実行されるのではなく、アクションおよび状態によってトリガーされます。 シーケンシャル ワークフローと同様に、ステート マシン ワークフローは、リストやドキュメントなどの SharePoint アイテムに関連付けられます。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できることも、シーケンシャル ワークフローと同じです。 ワークフローを自動的に開始するか手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [sharepoint ワークフローソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、「 [sharepoint Server 2010 のワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))」、および「 [新機能: ワークフローの機能強化](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))」を参照してください。

### <a name="user-control-farm-solution-only"></a>ユーザーコントロール (ファームソリューションのみ)
 *ユーザーコントロール*は、他の ASP.NET コントロールや SharePoint コントロールを追加できる、再利用可能なカスタムコントロールです。 ユーザー コントロールは、SharePoint で実行されるアプリケーション ページと Web パーツに追加できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「 [Web パーツまたはアプリケーションページの再利用可能なコントロールの作成](creating-reusable-controls-for-web-parts-or-application-pages.md)」を参照してください。

### <a name="visual-web-part"></a>視覚的 web パーツ
 *視覚的 web パーツ*プロジェクト項目には、 *Elements.xml*定義ファイル、 **Web パーツ**項目、および**ユーザーコントロール**項目が含まれます。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「方法: デザイナーとビルドブロックを [使用して SharePoint web パーツを作成](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) する [: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="web-part"></a>Web パーツ
 *Web パーツ*は、Web パーツページと呼ばれる特殊な種類のページ内で実行されるサーバー側コントロールです。 これらは、SharePoint サイトに表示されるページのビルド ブロックです。 Web パーツ項目には、SharePoint サイト用の Web パーツをデザインするためのファイルが用意されています。 詳細については、「 [How to: Create a SharePoint web part](../sharepoint/how-to-create-a-sharepoint-web-part.md) And [ビルディング Block: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint 製品とテクノロジ](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))
