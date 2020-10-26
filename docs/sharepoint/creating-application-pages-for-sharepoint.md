---
title: SharePoint 用のアプリケーションページを作成する |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web pages
- SharePoint development in Visual Studio, content pages
- SharePoint development in Visual Studio, application pages
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 47f403f4eec6ec66563ae88bec226e073f625716
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72981098"
---
# <a name="create-application-pages-for-sharepoint"></a>SharePoint のアプリケーションページの作成
  *アプリケーションページ*は、SharePoint web サイトで使用できるように設計された ASP.NET web ページです。 アプリケーションページは特殊な種類の ASP.NET ページです。 アプリケーションページと標準 ASP.NET ページの主な違いは、アプリケーションページに SharePoint マスターページとマージされたコンテンツが含まれていることです。 マスターページを使用すると、アプリケーションページは、サイト上の他のページと同じ外観と動作を共有できます。

 Visual Studio では、デザイナーを使用してアプリケーションページをデザインできます。 デザイナーには、マスターページで定義されている各コンテンツプレースホルダーのコンテンツ領域が表示されます。 これらのコンテンツ領域にコントロールをドラッグすることで、アプリケーションページをデザインできます。

## <a name="application-pages"></a>アプリケーションページ
 アプリケーションページは、サーバー上のすべてのサイトで共有されます。一方、サイトページは、1つのサイトに固有です。 詳細については、「 [SharePoint ページの種類](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))」を参照してください。

 既定では、SharePoint サイトを作成するときに表示されるページのほとんどは、サイトページです。 サイトページは、SharePoint ページライブラリに追加できます。 ユーザーは、SharePoint デザイナーなどのツールを使用してサイトページをカスタマイズできます。 サイトページでは、動的 Web パーツ、Web パーツゾーンなどの機能もホストできます。

 アプリケーションページでは、これらの処理を行うことはできません。 ただし、ページにカスタムコードを含める場合は、アプリケーションページを作成することをお勧めします。 サイトページにカスタムコードを追加できますが、ユーザーが SharePoint デザイナーなどのツールを使用してページをカスタマイズすると、コードの実行が停止します。

> [!NOTE]
> Visual Studio には、SharePoint サイトのサイトページを作成するのに役立つテンプレートは用意されていません。 詳細については、「 [SharePoint ページの種類](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))」を参照してください。

## <a name="create-an-application-page"></a>アプリケーションページを作成する
 アプリケーションページを作成するには、 **アプリケーションページ** アイテムを SharePoint プロジェクトに追加します。 アプリケーションページを作成すると、Visual Studio によって次のフォルダーがプロジェクトに追加されます。

|Folder|説明|
|------------|-----------------|
|レイアウト|SharePoint ファイルシステムの _layouts 仮想ディレクトリにマップされます。|
|レイアウトサブフォルダー|アプリケーションページを構成するファイルが含まれます。 既定では、このフォルダーの名前はプロジェクトと同じです。 このフォルダーの名前はいつでも変更できます。 プロジェクトを実行すると、Visual Studio によってこのフォルダーが SharePoint ファイルシステムの _layouts 仮想ディレクトリに配置されます。|

 Visual Studio によって、次のファイルがプロジェクトに追加されます。

|ファイル|説明|
|----------|-----------------|
|ASP.NET ページファイル (*.aspx*)|ページを定義する XML マークアップを格納します。|
|アプリケーションページのコードファイル|アプリケーションページの背後にあるコードを含みます。 イベントを処理するコードをこのファイルに追加します。|
|アプリケーションページデザイナーコードファイル|デザイナーによって生成されるコードが含まれています。 このファイルは直接編集しないでください。|

## <a name="design-and-debug-an-application-page"></a>アプリケーションページをデザインおよびデバッグする
 Visual Studio のデザイナービューを使用して、アプリケーションページの内容をデザインします。 このデザイナーは、プロジェクトのアプリケーションページを開いたときに表示されます (ダブルクリックするか、ショートカットメニューを開き、[ **開く**] をクリックします)。その後、エディターの下部にある [ **デザイン** ] ボタンをクリックします。

> [!NOTE]
> ページのデザインは、デザイナーの **ソース** ビューでのみ行うことができます。 デザイナーの **デザイン** ビューは、アプリケーションページでは無効になっています。

 Visual Studio で他の SharePoint プロジェクトアイテムをデバッグする場合と同じように、アプリケーションページをデバッグできます。 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 アプリケーションページを表示するには、アプリケーションページの場所 (例: http://<em>Server_Name</em>/_layouts/*Project_Name*/applicationpage1. aspx) に手動で移動する必要があります。

 SharePoint プロジェクトをデバッグする方法の詳細については、「 [sharepoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="choose-a-master-page"></a>マスターページの選択
 既定では、 **アプリケーションページ** アイテムは、プロジェクトのデバッグに使用しているサイトのマスターページを参照します。 このページには「v4. master」という名前が付けられ、SharePoint サイトの **マスターページギャラリー** に一覧表示されます。

 アプリケーションのページで使用されるマスターページは、application 要素の属性を設定することによって明示的に変更でき `MasterPageFile` `Page` ます。 (例: `MasterPageFile="~/_layouts/applicationv4.master"` )。 実際、SharePoint サーバーで動的なマスターページが有効になっていない場合は、この属性を設定する必要があります。 SharePoint のマスターページの詳細については、「 [マスターページ](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint Foundation 開発の詳細](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET の概要](/aspnet/overview)
- [ASP.NET Web ページ](/aspnet/web-pages/index)
