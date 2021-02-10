---
title: Visual Studio での Office および SharePoint 開発
description: ユーザーが Office ストアからダウンロードする軽量なアプリまたはアドインを作成することによって Microsoft Office と SharePoint を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], about developing applications
- Office development in Visual Studio
- Office projects
- Visual Studio Tools for Office, see Office development in Visual Studio
- Office applications [Office development in Visual Studio]
- Office Business Applications
- applications [Office development in Visual Studio]
- programming [Office development in Visual Studio]
- VSTO, see Office development in Visual Studio
- Office, development with Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cebcb16708e42f8102e2dc235b52a81e16c588c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940905"
---
# <a name="office-and-sharepoint-development-in-visual-studio"></a>Visual Studio での Office および SharePoint 開発
  ユーザーが [Office ストア](https://store.office.com/) または組織のカタログからダウンロードする軽量なアプリやアドインを作成するか、ユーザーがコンピューターにインストールする .NET Framework ベースのソリューションを作成することによって、Microsoft Office および SharePoint を拡張できます。

 このトピックの内容:

- [Office と SharePoint 用アドインの作成](#Apps)

- [VSTO アドインを作成する](#Add-ins)

- [SharePoint ソリューションの作成](#Solutions)

## <a name="create-add-ins-for-office-and-sharepoint"></a><a name="Apps"></a> Office と SharePoint 用アドインの作成
 Office 2013 と SharePoint 2013 では、Office と SharePoint を拡張するためのアドインを構築、配布、収益化するために役立つ新しいアドイン モデルが導入されます。  これらのアドインは、Office Online または SharePoint Online で実行でき、ユーザーは多くのデバイスからアプリと対話できます。

 新しい [Office アドインモデル](/office/dev/add-ins/overview/office-add-ins) を使用してユーザーの office エクスペリエンスを拡張する方法について説明します。

 これらのアドインのフットプリントは、VSTO アドインやソリューションと比較して小さく、HTML5、JavaScript、CSS3、XML など、ほぼすべての web プログラミングテクノロジを使用してビルドすることができます。  作業を開始するには、Visual Studio の Office Developer Tools を使用します。これにより、プロジェクトの作成、コードの記述、およびブラウザーでのアドインの実行を行うことができます。

 ![Office 用アプリと SharePoint 用アプリの概念モデル](../vsto/media/officeandsharepointapps2015.png "Office 用アプリと SharePoint 用アプリの概念モデル")

### <a name="build-an-office-add-in"></a>Office アドインをビルドする
 Office の機能を拡張するには、Office アドインを構築します。 基本的には、Excel、Word、Outlook、PowerPoint などの Office アプリケーションでホストされている web ページです。 構築したアプリを使用して、ドキュメント、ワークシート、電子メール メッセージ、予定、プレゼンテーション、およびプロジェクトに機能を追加できます。

 構築したアプリは Office ストアで販売できます。  [Office ストア](https://store.office.com/) を使用すると、アドインの収益化、更新プログラムの管理、および利用統計情報の追跡が簡単になります。 また、SharePoint のアプリ カタログや Exchange Server 上で、アプリをユーザーに公開することもできます。

 Bing マップ内にワークシートのデータを表示する Office 向けアプリを次に示します。

 ![Office 用のコンテンツ アプリ](../vsto/media/appforoffice.png "Office 用のコンテンツ アプリ")

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|Office アドインの詳細を確認し、アドインを構築する。|[Office アドイン](/office/dev/add-ins/publish/publish)|
|Office のさまざまな拡張方法を比較し、アプリと Office アドインのどちらを使用する必要があるかを判断する。|[Office アドイン、VSTO、および VBA のロードマップ](/archive/blogs/officeapps/roadmap-for-apps-for-office-vsto-and-vba)|

### <a name="build-a-sharepoint-add-in"></a>SharePoint アドインの作成
 ユーザー向けに SharePoint を拡張するには、SharePoint アドインを構築します。 これは基本的に、ユーザーまたはビジネスのニーズを解決する、小規模で使いやすいスタンドアロンアプリケーションです。

 構築した SharePoint 用のアプリは [Office ストア](https://store.office.com/)で販売できます。 また、SharePoint のアドイン カタログを使用して、アドインをユーザーに公開することもできます。  サイト所有者は、ファーム サーバーやサイト コレクションの管理者の助けを借りることなく、アドインを SharePoint サイトにインストール、アップグレード、およびアンインストールできます。

 ユーザーがビジネスの連絡先を管理するのに役立つ SharePoint 用アプリの例を次に示します。

 ![SharePoint 用 Business Contact Manager アプリ](../vsto/media/appforsharepoint.png "SharePoint 用 Business Contact Manager アプリ")

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|SharePoint アドインの詳細を確認し、アドインを構築する。|[SharePoint アドイン](/sharepoint/dev/sp-add-ins/sharepoint-add-ins)|
|SharePoint アドインを従来の SharePoint ソリューションと比較する。|[Sharepoint アドインと SharePoint ソリューションの比較](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|
|SharePoint ソリューションと SharePoint アドインのどちらを構築するかを選択する。|[SharePoint アドインと SharePoint ソリューションの決定](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|

## <a name="create-a-vsto-add-in"></a><a name="Add-ins"></a> VSTO アドインを作成する
 Office 2007 または Office 2010 を対象とする VSTO アドインを作成するか、office 2013 と office 2016 を拡張して、office アドインでは実現できないようにします。VSTO アドインはデスクトップ上でのみ実行されます。 ユーザーは VSTO アドインをインストールする必要があるため、通常は配置とサポートが難しくなります。  ただし、VSTO アドインは、より密接に Office に統合できます。 たとえば、Office リボンにタブやコントロールを追加し、文書の結合やグラフの変更などの高度な自動化タスクを実行できます。 また、.NET Framework を活用し、C# および Visual Basic を使用して、Office オブジェクトと対話することもできます。

 VSTO アドインで実行できる機能の例を次に示します。 この VSTO アドインは、PowerPoint にリボン コントロール、カスタム作業ウィンドウ、およびダイアログ ボックスを追加します。

 ![PowerPoint アドインソリューション](../vsto/media/powerpointaddin.png "PowerPoint アドイン ソリューション")

 **詳細情報**

|終了|Read|
|--------|----------|
|Office のさまざまな拡張方法を比較し、VSTO アドインと Office アドインのどちらを使用する必要があるかを判断する。|[Office アドイン、VSTO、および VBA のロードマップ](/archive/blogs/officeapps/roadmap-for-apps-for-office-vsto-and-vba)|
|VSTO アドインを作成する。|[Visual Studio で作成した VSTO アドイン](create-vsto-add-ins-for-office-by-using-visual-studio.md)|

## <a name="create-a-sharepoint-solution"></a><a name="Solutions"></a> SharePoint ソリューションの作成
 Sharepoint Foundation 2010 と SharePoint Server 2010 を対象とする SharePoint ソリューションを作成したり、sharepoint 2013 と SharePoint 2016 を SharePoint アドインでは実現できない方法で拡張したりすることができます。

 SharePoint ソリューションには、内部設置型の SharePoint ファーム サーバーが必要です。 管理者はソリューションをインストールする必要があります。また、ソリューションは SharePoint 内で実行されるため、サーバーのパフォーマンスに影響を与える可能性があります。 ただし、ソリューションでは、より深いレベルの SharePoint オブジェクトへのアクセスが提供されます。 また、SharePoint ソリューションの構築時に、.NET Framework を活用し、C# および Visual Basic を使用して、SharePoint オブジェクトと対話できます。

 **詳細情報**

|終了|解決方法については、|
|--------|---------|
|SharePoint ソリューションを SharePoint アドインと比較する。|[Sharepoint アドインと SharePoint ソリューションの比較](/sharepoint/dev/general-development/sharepoint-server-application-lifecycle-management)|
|SharePoint ソリューションを作成する。|[SharePoint ソリューションの作成](../sharepoint/create-sharepoint-solutions.md)|