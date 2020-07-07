---
title: SharePoint のサイト定義を作成する |Microsoft Docs
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
ms.openlocfilehash: 0f1a512218c3c1b7af179cfaba3e231a90941fe0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015067"
---
# <a name="create-site-definitions-for-sharepoint"></a>SharePoint のサイト定義の作成
  の SharePoint サイト定義プロジェクトでは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 新しい sharepoint サイトの基礎として機能する*サイト定義*を作成できます。 これらの定義では、SharePoint サイトの外観と動作だけでなく、既定のコンテンツと機能も決定されます。 定義では、事前に構成されたリスト、コンテンツタイプ、イベントレシーバー、画像、およびその他のアイテムを含めることができます。 SharePoint には、たとえば、ブログなどのいくつかのサイト定義が含まれています。 ブログサイト定義に基づいてサイトを作成する場合、サイトには、ブログサイトに必要なリスト、Web パーツ、およびその他のアイテムが含まれています。

 サイト定義の詳細については、「[サイトテンプレートと定義](/previous-versions/office/developer/sharepoint-2010/ms434313(v=office.14))」を参照してください。

## <a name="site-definition-projects"></a>サイト定義プロジェクト
 のサイト定義プロジェクトは [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint サイトに必要な基本的なファイルのみを提供します。既定の機能は提供されません。 必要な機能を提供するために、ファイルとコンテンツを追加する必要があります。 必要なファイルを作成して追加することによって、サイトを手動でビルドできます。

## <a name="feature-stapling"></a>機能のホチキス止め
 でサイト定義を作成する利点の1つ [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は、*機能のホチキス止め*を自動的に使用することです。 機能のホチキス止めは、サイト定義自体に機能を埋め込むのではなく、サイト定義に機能をアタッチします。 これにより、元のサイト定義を変更せずに、サイト定義を使用して作成されたサイトに機能を追加できます。 詳細については、「[機能のホチキス止め](/previous-versions/office/developer/sharepoint-2007/bb861862(v=office.12))」を参照してください。

## <a name="site-definition-project-components"></a>サイト定義プロジェクトコンポーネント
 サイト定義ソリューションを作成すると、次の既定のファイルが**Sitedefinition**ノードに追加されます。

|ファイル名|説明|
|---------------|-----------------|
|*default.aspx*|新しい SharePoint サイトの既定の ASPX ホームページ。|
|*onet.xml*|新しいサイトの構成、サイト定義テンプレートのコンポーネント、および既定の動作を指定します。 これらの設定には、有効になっているコンテンツの種類、既定のリストビュー、ドキュメントテンプレートファイル、およびサイトに含まれる Web パーツなどの属性を含めることができます。 既定では、このセクションには、 `Modules` SharePoint サイトに追加するファイルとその構成方法が一覧表示されます。|
|*webtemp_ \<SiteDefinitionName> .xml*|[**新しい SharePoint サイト**] ページの [**テンプレートの選択**] セクションに表示されるサイト定義の構成を指定します。|

 既定では、すべてのサイト定義は、 * \<drive:> Files\Common の Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates*フォルダーに格納されます。 各サイト定義には、独自のサブフォルダーがあります。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: 基本サイト定義プロジェクトの作成](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|で基本的なサイト定義プロジェクトを作成する手順について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。|
|[方法: カスタムサイト定義と構成を作成する](/previous-versions/office/developer/sharepoint-2010/ms454677(v=office.14))|既存のサイト定義をコピーし、そのコピーを変更することによって、SharePoint でカスタムサイト定義を作成する方法について説明します。|
|[*WebTemp.xml*](/previous-versions/office/developer/sharepoint-2010/ms447717(v=office.14))|[**新しい SharePoint サイト**] ページの [**テンプレートの選択**] セクションで使用できるサイト定義を指定する元のファイルについて説明します。|
|[SharePoint ソリューションのローカライズ](../sharepoint/localizing-sharepoint-solutions.md)|SharePoint ソリューションをグローバルに使用できるように準備する方法について説明します。|
|[SharePoint の web パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md)|SharePoint ページの一部を作成して、ユーザーが変更できるようにする方法について説明します。|
|[Web パーツまたはアプリケーションページの再利用可能なコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|アプリケーションページおよび Web パーツで実行される再利用可能なコントロールを作成する方法について説明します。|
|[Visual Web Developer](/previous-versions/visualstudio/visual-studio-2010/ms178093(v=vs.100))|プロジェクトで Web ページを開いたときに表示されるデザイナーの使用方法について説明します。|
|[ASP.NET Web ページの概要](/previous-versions/aspnet/428509ah(v=vs.100))|Web ページの構造、 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] でページがどのように処理されるか、 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] および [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] XHTML 標準に準拠しているマークアップをページがどのように表示するかに関する一般的な情報を提供します。|
|[ASP.NET Web ページの構文](/previous-versions/aspnet/k33801s3(v=vs.100))|ASP.NET ページを構成するマークアップ要素について説明します。|
|[プログラミング ASP.NET Web ページ](/previous-versions/aspnet/0yt4zca8(v=vs.100))|ページでイベントハンドラーを作成する方法 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] と、クライアントスクリプトを使用する方法について説明します。|
|[Windows SharePoint Services でのプログラミング](/previous-versions/office/developer/sharepoint-services/ms430674(v=office.12))|に用意されているマネージオブジェクトモデルの使用方法について説明し [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] ます。|

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
