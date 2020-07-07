---
title: SharePoint 用のページを作成する |Microsoft Docs
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 942891bc9281c07966160ea9df065408fcbfd5ff
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015167"
---
# <a name="create-pages-for-sharepoint"></a>SharePoint のページを作成する
  SharePoint サイトのアプリケーションページ、サイトページ、マスターページ、およびページレイアウトを作成できます。

 アプリケーションページは、Visual Studio のテンプレートを使用して作成できます。 SharePoint Designer を使用して、サイトページ、マスターページ、およびページレイアウトを作成します。 次に、これらのページを Visual Studio にインポートして、SharePoint プロジェクトで使用できます。

 カスケードスタイルシート、ECMAScript、およびテーマを使用して、ページの外観と動作を変更することもできます。

## <a name="types-of-sharepoint-pages"></a>SharePoint ページの種類
 次の表では、SharePoint サイトに含まれる4種類のページについて説明します。

|ページの種類|説明|
|---------------|-----------------|
|アプリケーションページ|ページにカスタムコードを含める場合、またはページを複数のサイトで共有する場合は、アプリケーションページを作成します。 それ以外の場合は、サイトページが最適な選択肢となることがあります。|
|サイトページ|次のいずれかのタスクを実行する場合は、サイトページを作成します。<br /><br /> -SharePoint ライブラリにページを追加します。<br />-動的 Web パーツ、Web パーツゾーンなどの機能をホストするためにページを有効にします。<br />-ユーザーが SharePoint デザイナーを使用してページをカスタマイズできるようにします。<br /><br /> ページにカスタムコードを含める場合は、サイトページを作成しないでください。 サイトページにカスタムコードを追加できますが、ユーザーが SharePoint デザイナーを使用してページをカスタマイズすると、コードの実行が停止します。|
|マスターページ|サイトページとアプリケーションページの共通構造を定義する場合は、マスターページを作成します。|
|ページ レイアウト|ページレイアウトはに固有 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] であり、サイトページとアプリケーションページの共通構造をさらに定義することができます。|

 ページの種類の概要については、「[構成要素: ページとユーザーインターフェイス](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))」と「[ページレイアウトとマスターページ](/previous-versions/office/developer/sharepoint-2010/ms543497(v=office.14))」を参照してください。

## <a name="create-application-pages"></a>アプリケーションページの作成
 アプリケーション**ページ**アイテムを SharePoint プロジェクトに追加することにより、Visual Studio でアプリケーションページを作成できます。 コントロールをページに追加し、コードを追加することによってコントロールイベントを処理できます。

 ページのコードファイルにブレークポイントを設定し、デバッガーを起動して、追加の構成手順を実行せずに、ローカルの SharePoint サイトでページをテストすることができます。 詳細については、「 [SharePoint のアプリケーションページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)」を参照してください。

## <a name="create-site-pages-master-pages-and-page-layouts"></a>サイトページ、マスターページ、およびページレイアウトの作成
 SharePoint Designer を使用して、サイトページ、マスターページ、およびページレイアウトを作成できます。 次に、これらのページを Visual Studio にインポートできます。 Visual Studio で使用可能な配置機能またはソース管理機能を利用する場合は、ページをインポートします。 詳細については、「[既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

 これらのページをインポートした後に変更するのは難しいため、インポートする前にこれらのページをデザインする必要があります。

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>カスケードスタイルシート、ECMAScript、およびテーマを作成する
 Visual Studio には、SharePoint サイトのカスケードスタイルシート (CSS)、ECMAScript (JavaScript、JScript)、またはテーマファイルを開発するためのテンプレートは用意されていません。 これらのファイルを作成するには、SharePoint SDK で利用可能なガイダンスを使用するか、SharePoint デザイナーなどのツールを使用します。

 これらのファイルをソリューションに直接追加することも、インポートすることもできます。 どちらの場合も、追加する各項目に対して適切にマップされたフォルダーを作成する必要があります。 マップされたフォルダーを作成する方法の詳細については、「[方法: マップされたフォルダーを追加および削除](../sharepoint/how-to-add-and-remove-mapped-folders.md)する」を参照してください。

 カスケードスタイルシートの作成の詳細については、「 [SharePoint Foundation のカスケードスタイルシートクラスの使用法](/previous-versions/office/developer/sharepoint-2010/ms438349(v=office.14))」を参照してください。 SharePoint ソリューションの JavaScript ファイルと JScript ファイルの作成の詳細については、「 [ECMAScript 用の基本的な ASPX ページの設定](/previous-versions/office/developer/sharepoint-2010/ee535709(v=office.14))」を参照してください。 テーマの詳細については、「[構成要素: ページ」と「ユーザーインターフェイス](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[SharePoint のアプリケーションページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)|SharePoint マスターページとマージされるアプリケーションページ ( *.aspx*コンテンツ) を追加する方法について説明します。|
|[方法: アプリケーションページを作成する](../sharepoint/how-to-create-an-application-page.md)|SharePoint サイトで実行される ASP.NET ページを作成する方法について説明します。|
|[チュートリアル: SharePoint アプリケーションページの作成](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|SharePoint サイトの ASP.NET Web ページをデザインおよびデバッグする方法について説明します。|
