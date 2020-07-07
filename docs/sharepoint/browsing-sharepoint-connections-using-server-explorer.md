---
title: サーバーエクスプローラーを使用した SharePoint 接続の参照 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.SharePointExplorer.SharePointConnection
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: baf580ace98ab14032de1e9a3edf18af2b2cfee8
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016353"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>サーバーエクスプローラーを使用した SharePoint 接続の参照
  **サーバーエクスプローラー**でローカル SharePoint 接続を参照できるようになりました。 この手法を使用すると、システム上の SharePoint サイトのコンポーネント間を移動できます。 リスト定義やコンテンツの種類などの SharePoint サイトコンポーネントは、**サーバーエクスプローラー**のツリービューで**sharepoint 接続**という名前のノードに表示されます。 **サーバーエクスプローラー**を表示するには、メニューバーで [サーバーエクスプローラーの**表示**] を選択し  >  **Server Explorer**ます。 SharePoint サイトコンポーネントの表示に加えて、アイテムの削除、プロパティの表示、またはショートカットメニューのコマンドを使用したツリービューの更新を行うことができます。

> [!IMPORTANT]
> SharePoint サイトを参照するには、SharePoint サイトコレクションの管理者である必要があります。また、ローカルコンピューターの管理者として Visual Studio を実行している必要があります。 それ以外の場合、サイトは**サーバーエクスプローラー**に表示されますが、ノードを展開することはできません。 サイトコレクションの管理者であるかどうかを確認するには、web ブラウザーでサイトを開き、[**サイトの操作**] メニューを開き、[**サイトのアクセス許可**] を選択します。次に、[**アクセス許可: チームサイト**] ページで、リボンの [**管理**] グループの [**サイトコレクションの管理者**] コマンドを選択します。 サイトコレクションの管理者である場合は、テキストボックスに名前が表示されます。 [**サイトコレクションの管理者**] コマンドがリボンの [管理] グループに表示されない場合は、サイトコレクションの管理者ではなく、サイト管理者から適切なアクセス許可を取得する必要があります。

## <a name="server-explorer-nodes"></a>ノードのサーバーエクスプローラー
 SharePoint サイトのすべてのコンポーネントは、[ **Sharepoint 接続**] の下の**サーバーエクスプローラー**ツリービューのノードによって表されます。 たとえば、既定の SharePoint サイトには、ディスカッションと呼ばれるコンテンツの種類が含まれます。これは、SharePoint サイトの [**ディスカッション**] ページに表示されるディスカッションの種類を表します。 ディスカッションコンテンツの種類には、いくつかのフィールドが含まれています。 これらのフィールドを**サーバーエクスプローラー**で表示するには、[**コンテンツ**] ノードを展開し、[**ディスカッション**] ノードを展開します。 その下には、本文、ディスカッションの件名、タイトルなど、いくつかのフィールドノードがあります。

## <a name="node-shortcut-menu-commands"></a>ノードのショートカットメニューのコマンド
 各ノードには、ノードを右クリックするか選択してから**Shift**F10 キーを押すことによってアクセスできるショートカットメニューがあり + **F10**ます。 ノードのコマンドには、次のようなものがあります。

|コマンド名|説明|
|------------------|-----------------|
|更新|ノードが最後に表示されてから発生した可能性のある変更を反映するように、ツリービューを更新します。|
|削除|選択したノードをツリービューから削除します。 **注:** このコマンドは、[ **Sharepoint 接続**] ノードの下に一覧表示されている sharepoint 接続でのみ有効です。|
|Properties|選択したノードの使用可能なプロパティが [**プロパティ**] ウィンドウに表示されます。 プロパティはすべて読み取り専用であり、すべてのノードにプロパティが関連付けられているわけではありません。|
|接続の追加|参照する SharePoint サイトを指定できます。 [ **SharePoint 接続**] ノードとサブサイトノードで使用できます。|
|ブラウザーで表示|選択したリストを Web ブラウザーに表示します。 このコマンドは、リスト**およびライブラリ**に含まれる [**リスト**] ノードの下にあるいくつかの一覧で使用できます。|

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: SharePoint 接続を追加または削除する](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|**サーバーエクスプローラー**の [ **sharepoint 接続**ノードに新しい sharepoint サイトを追加するために必要な手順について説明します。|

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
