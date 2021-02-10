---
title: SharePoint 用ページの作成 | Microsoft Docs
description: アプリケーション ページは、Visual Studio のテンプレートを使用して作成します。 サイト ページ、マスター ページ、およびページ レイアウトは、SharePoint Designer を使用して作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, master pages
- SharePoint development in Visual Studio, page layouts
- SharePoint development in Visual Studio, content pages
- master pages[SharePoint development in Visual Studio], designing
- content pages[SharePoint development in Visual Studio], designing
- page layouts[SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 702d2c4d5cafd6f4ff4ef2e4104da9f6cc02c5fb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949169"
---
# <a name="create-pages-for-sharepoint"></a>SharePoint のページを作成する
  SharePoint サイト用のアプリケーション ページ、サイト ページ、マスター ページ、およびページ レイアウトを作成できます。

 アプリケーション ページは、Visual Studio のテンプレートを使用して作成できます。 サイト ページ、マスター ページ、およびページ レイアウトは、SharePoint Designer を使用して作成します。 次に、これらのページを Visual Studio にインポートして、SharePoint プロジェクトで使用できます。

 カスケード スタイル シート、ECMAScript、およびテーマを使用して、ページの外観と動作を変更することもできます。

## <a name="types-of-sharepoint-pages"></a>SharePoint ページの種類
 次の表では、SharePoint サイトに含まれる主な 4 種類のページについて説明します。

|ページの種類|説明|
|---------------|-----------------|
|アプリケーション ページ|アプリケーション ページは、ページにカスタム コードを含める場合、またはページを複数のサイトで共有する場合に作成します。 それ以外の場合は、サイト ページが最適な選択肢となることがあります。|
|サイト ページ|サイト ページは、次のいずれかのタスクを実行する場合に作成します。<br /><br /> -   ページを SharePoint ライブラリに追加する。<br />-   動的 Web パーツや Web パーツ ゾーンなどの機能をページでホストできるようにする。<br />-   ユーザーが SharePoint Designer を使用してページをカスタマイズできるようにする。<br /><br /> ページにカスタム コードを含める場合は、サイト ページを作成しないでください。 サイト ページにカスタム コードを追加することはできますが、ユーザーが SharePoint Designer を使用してページをカスタマイズすると、コードの実行が停止します。|
|マスター ページ|マスター ページは、サイト ページとアプリケーション ページの共通構造を定義する場合に作成します。|
|ページ レイアウト|ページ レイアウトは [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] に固有のものであり、サイト ページとアプリケーション ページの共通構造をさらに定義することができます。|

 ページの各種類の概要については、「[文書パーツ: ページとユーザー インターフェイス](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))」、および「[ページ レイアウトとマスター ページ](/previous-versions/office/developer/sharepoint-2010/ms543497(v=office.14))」を参照してください。

## <a name="create-application-pages"></a>アプリケーション ページを作成する
 **アプリケーション ページ** 項目を SharePoint プロジェクトに追加することにより、Visual Studio でアプリケーション ページを作成できます。 コントロールをページに追加し、コードを追加することによってコントロール イベントを処理できます。

 ページのコード ファイルにブレークポイントを設定し、デバッガーを起動して、追加の構成手順を実行せずに、ローカルの SharePoint サイトでページをテストすることができます。 詳細については、「[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)」を参照してください。

## <a name="create-site-pages-master-pages-and-page-layouts"></a>サイト ページ、マスター ページ、およびページ レイアウトを作成する
 SharePoint Designer を使用して、サイト ページ、マスター ページ、およびページ レイアウトを作成できます。 次に、これらのページを Visual Studio にインポートできます。 Visual Studio で使用可能な配置機能またはソース管理機能を利用する場合は、ページをインポートします。 詳細については、「[既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

 これらのページをインポートした後に変更するのは難しいため、インポートする前にこれらのページをデザインする必要があります。

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>カスケード スタイル シート、ECMAScript、およびテーマを作成する
 Visual Studio には、SharePoint サイト用のカスケード スタイル シート (CSS)、ECMAScript (JavaScript、JScript)、またはテーマ ファイルを開発するためのテンプレートは用意されていません。 これらのファイルは、SharePoint SDK で利用可能なガイダンスを使用して、または SharePoint Designer などのツールを使用して作成できます。

 これらのファイルをソリューションに直接追加することも、インポートすることもできます。 どちらの場合も、追加する各項目に対して適切にマップされたフォルダーを作成する必要があります。 マップされたフォルダーを作成する方法の詳細については、「[方法: マップされたフォルダーを追加および削除する](../sharepoint/how-to-add-and-remove-mapped-folders.md)」を参照してください。

 カスケード スタイル シートの作成の詳細については、「[SharePoint Foundation におけるカスケード スタイル シート クラスの使用](/previous-versions/office/developer/sharepoint-2010/ms438349(v=office.14))」を参照してください。 SharePoint ソリューション用の JavaScript および JScript ファイルの作成の詳細については、[ECMAScript を使用する基本的な ASPX ページの設定](/previous-versions/office/developer/sharepoint-2010/ee535709(v=office.14))に関するページを参照してください。 テーマの詳細については、「[文書パーツ: ページとユーザー インターフェイス](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)|アプリケーション ページ (SharePoint マスター ページとマージされた *.aspx* コンテンツ) を追加する方法について説明します。|
|[方法: アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)|SharePoint サイトで実行される ASP.NET ページを作成する方法について説明します。|
|[チュートリアル: SharePoint アプリケーション ページの作成](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|SharePoint サイトの ASP.NET Web ページをデザインおよびデバッグする方法について説明します。|
