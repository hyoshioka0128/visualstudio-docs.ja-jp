---
title: SharePoint のサイト定義の作成 | Microsoft Docs
description: SharePoint のサイト定義を作成します。 サイト定義によって、SharePoint サイトの外観と動作、およびその既定のコンテンツと機能が決まります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7585a4b80322afb37e816758fc7074806a443676
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850573"
---
# <a name="create-site-definitions-for-sharepoint"></a>SharePoint のサイト定義を作成する
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の SharePoint サイト定義プロジェクトを使用すると、新しい SharePoint サイトの基盤として機能する "*サイト定義*" を作成できます。 これらの定義によって、SharePoint サイトの外観と動作だけでなく、その既定のコンテンツと機能も決まります。 定義には、事前に構成された一覧、コンテンツ タイプ、イベント レシーバー、イメージ、およびその他の項目を含めることができます。 SharePoint には、たとえば、ブログなどのいくつかのサイト定義が含まれています。 ブログ サイト定義に基づいてサイトを作成する場合、そのサイトには、ブログ サイトに必要なリスト、Web パーツ、およびその他の項目が含まれます。

 サイト定義の詳細については、[サイトのテンプレートと定義](/previous-versions/office/developer/sharepoint-2010/ms434313(v=office.14))に関するページを参照してください。

## <a name="site-definition-projects"></a>サイト定義プロジェクト
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のサイト定義プロジェクトでは、SharePoint サイトに必要な基本的なファイルのみが提供されます。既定の機能は提供されません。 必要な機能を用意するには、ファイルとコンテンツを追加する必要があります。 必要なファイルを作成して追加することによって、サイトを手動で構築できます。

## <a name="feature-stapling"></a>機能の関連付け
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でサイト定義を作成する利点の 1 つは、"*機能の関連付け*" が自動的に使用されることです。 機能の関連付けを使用すると、サイト定義自体にその機能が埋め込まれるのではなく、サイト定義に機能がアタッチされます。 これにより、元のサイト定義を変更せずに、サイト定義を使用して作成されたサイトに機能を追加できます。 詳細については、「[機能の関連付け](/previous-versions/office/developer/sharepoint-2007/bb861862(v=office.12))」を参照してください。

## <a name="site-definition-project-components"></a>サイト定義プロジェクトのコンポーネント
 サイト定義ソリューションを作成すると、次の既定のファイルがその **SiteDefinition** ノードに追加されます。

|ファイル名|説明|
|---------------|-----------------|
|*default.aspx*|新しい SharePoint サイトの既定の ASPX ホーム ページ。|
|*onet.xml*|新しいサイトの構成、サイト定義テンプレートのコンポーネント、および既定の動作を指定します。 これらの設定には、有効になっているコンテンツの種類、既定のリスト ビュー、ドキュメント テンプレート ファイル、およびサイトに含まれる Web パーツなどの属性を含めることができます。 既定では、`Modules` セクションで、SharePoint サイトに追加されるファイルとその構成方法が一覧表示されます。|
|*webtemp_\<SiteDefinitionName>.xml*|**[新しい SharePoint サイト]** ページの **[テンプレートの選択]** セクションに表示されるサイト定義構成を指定します。|

 既定では、すべてのサイト定義が *\<drive:>\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates* フォルダーに格納されます。 各サイト定義には、独自のサブフォルダーがあります。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: 基本サイト定義プロジェクトの作成](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で基本的なサイト定義プロジェクトを作成する手順について説明します。|
|[方法: カスタム サイト定義と構成を作成する](/previous-versions/office/developer/sharepoint-2010/ms454677(v=office.14))|既存のサイト定義をコピーしてから、そのコピーを変更することによって、SharePoint でカスタム サイト定義を作成する方法について説明します。|
|[*WebTemp.xml*](/previous-versions/office/developer/sharepoint-2010/ms447717(v=office.14))|**[新しい SharePoint サイト]** ページの **[テンプレートの選択]** セクションで使用できるサイト定義を指定する元のファイルについて説明します。|
|[SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)|SharePoint ソリューションをグローバルに使用できるように準備する方法について説明します。|
|[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)|ユーザーが変更できる SharePoint ページの一部をどのように作成できるかについて説明します。|
|[Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|アプリケーション ページおよび Web パーツで実行される再利用可能なコントロールを作成する方法について説明します。|
|[Visual Web Developer](/previous-versions/visualstudio/visual-studio-2010/ms178093(v=vs.100))|プロジェクトで Web ページを開くと表示されるデザイナーの使用方法について説明します。|
|[ASP.NET Web ページの概要](/previous-versions/aspnet/428509ah(v=vs.100))|[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] Web ページの構造、[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] によるページの処理方法、および XHTML 標準に準拠したマークアップを [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ページで表示する方法に関する一般的な情報を提供します。|
|[ASP.NET Web ページの構文](/previous-versions/aspnet/k33801s3(v=vs.100))|ASP.NET ページを構成するマークアップ要素について説明します。|
|[ASP.NET Web ページのプログラミング](/previous-versions/aspnet/0yt4zca8(v=vs.100))|[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] ページでイベント ハンドラーを作成する方法と、クライアント スクリプトを使用する方法に関する情報を提供します。|
|[Windows SharePoint Services でのプログラミング](/previous-versions/office/developer/sharepoint-services/ms430674(v=office.12))|[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] で提供されているマネージド オブジェクト モデルの使用方法について説明します。|

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
