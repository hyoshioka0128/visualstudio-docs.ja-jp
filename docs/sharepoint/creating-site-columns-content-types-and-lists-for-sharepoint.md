---
title: SharePoint 用のサイト列、コンテンツタイプ、およびリストの作成 |Microsoft Docs
titleSuffix: ''
description: SharePoint のサイト列、コンテンツタイプ、およびリストを作成します。 Visual Studio には、これらの種類の SharePoint アイテムのプロジェクトアイテムテンプレートが用意されています。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.ContentTypeSetting
- VS.SharePointTools.ContentTypeDesigner.CommonPropertiesPage
- VS.SharePointTools.ListDesigner.CreatingLists
- VS.SharePointTools.ListDesigner.ListPage
- VS.SharePointTools.ListDesigner.ViewPage
- VS.SharePointTools.ListDesigner.CommonPropertiesPage
- VS.SharePointTools.ContentTypeDesigner.ColumnsPage
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 29d0ebc33bf3df198f3ee9b3f9d80a747087341c
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850521"
---
# <a name="create-site-columns-content-types-and-lists-for-sharepoint"></a>SharePoint のサイト列、コンテンツ タイプ、リストの作成
  Visual Studio には、 *リスト* や *コンテンツの種類* など、さまざまな基本的な SharePoint アイテムのプロジェクトアイテムテンプレートが用意されています。このテンプレートには、サイトの列 (または *フィールド*) を組み込むことができます。 コンテンツの種類とリストの新しい設計者は、これらの項目をこれまで以上に簡単に作成できるようにします。

## <a name="site-columns"></a>サイト内の列
 サイト列は、SharePoint プロジェクトに追加できる最も基本的な要素の1つです。 サイト列は、連絡先リストに含まれる連絡先の電話番号、コメント、市区町村名などのデータの種類を表します。

 [新しいサイト列] プロジェクト項目テンプレートを使用すると、以前のバージョンの Visual Studio よりも簡単にサイト列を作成できます。 新しいサイト列を作成した後、サイト列の *Elements.xml* ファイル内の XML を変更して、表示名、データ型、SharePoint にサイト列を表示するグループなど、目的の情報を含めることができます。 サイト列の詳細については、「 [列の概要](/previous-versions/office/developer/sharepoint-2010/ms450825(v=office.14))」を参照してください。

## <a name="content-types-and-lists"></a>コンテンツの種類とリスト
 コンテンツの種類とリストは、SharePoint で最も頻繁に使用される要素の中にあります。

 コンテンツタイプは、SharePoint リストまたはドキュメントライブラリ内のアイテムのカテゴリのメタデータ、ワークフロー、および動作を定義します。 たとえば、連絡先リストまたはタスクリストの情報に対してコンテンツの種類を作成できます。 連絡先のコンテンツの種類には、名前、電子メール、電話番号、住所などの列が含まれる場合があります。 サイトレベルで定義するコンテンツの種類は、サイト内のどのリストまたはドキュメントライブラリからも独立しています。 SharePoint サイトの別のリストまたはドキュメントライブラリで同じコンテンツの種類を使用できます。 また、同じリストまたはドキュメントライブラリに複数のコンテンツの種類を使用することもできます。

 リストは、他のユーザーと共有できる SharePoint 内の情報のコレクションです。 リストは、データを含む列の行で構成されます。 リストの例としては、タスク一覧、連絡先リスト、お知らせリストなどがあります。

 の新しいコンテンツの種類とリストデザイナーに [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] より、以前のバージョンの Visual Studio よりもはるかに簡単で直感的なサイトコンテンツの種類とリストが作成されます。 UI では、使い慣れた方法でコンテンツの種類とリストを視覚的に作成できます。また、リストのデータを並べ替えたり、グループの見出しを使用したりすることができます。 コンテンツの種類の詳細については、「 [コンテンツの種類](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))」を参照してください。 リストの詳細については、「フォームと[リストビュー](/previous-versions/office/developer/sharepoint-2010/ff604021(v=office.14))の[一覧](/previous-versions/office/developer/sharepoint-2010/aa543232(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|カスタムコンテンツタイプで使用されるサイト列を作成する方法を示します。 コンテンツタイプは、カスタムリストで使用されます。|

## <a name="see-also"></a>関連項目
- [SharePoint 2010 で開発を開始する](/sharepoint/dev/)
