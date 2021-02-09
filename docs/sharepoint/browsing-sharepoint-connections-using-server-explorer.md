---
title: サーバー エクスプローラーを使用した SharePoint 接続の参照 | Microsoft Docs
description: サーバー エクスプローラーを使用して SharePoint 接続を参照します。 サーバー エクスプローラー ノードとノードのショートカット メニュー コマンドについて説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b188d95e6478e488fc896b0622fb8d145ef2a741
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851609"
---
# <a name="browse-sharepoint-connections-by-using-server-explorer"></a>サーバー エクスプローラーを使用して SharePoint 接続を参照する
  **サーバー エクスプローラー** でローカルの SharePoint 接続を参照できるようになりました。 この手法を使用すると、システム上の SharePoint サイトのコンポーネント間を移動できます。 リスト定義やコンテンツの種類などの SharePoint サイト コンポーネントは、**サーバー エクスプローラー** のツリー ビューで **[SharePoint 接続]** という名前のノードに表示されます。 **サーバー エクスプローラー** を表示するには、メニューバーで **[表示]**  >  **[サーバー エクスプローラー]** の順に選択します。 ショートカット メニューのコマンドを使用すると、SharePoint サイト コンポーネントの表示だけでなく、項目の削除、プロパティの表示、またはツリー ビューの更新を行うことができます。

> [!IMPORTANT]
> SharePoint サイトを参照するには、SharePoint サイト コレクションの管理者である必要があります。また、ローカル コンピューターの管理者として Visual Studio を実行している必要があります。 それ以外の場合、サイトは **サーバー エクスプローラー** に表示されますが、そのノードを展開することはできません。 サイト コレクションの管理者であるかどうかを確認するには、Web ブラウザーでサイトを開き、 **[サイト アクション]** メニューを開き、 **[サイトのアクセス許可]** を選択してから **[アクセス許可: チーム サイト]** ページで、リボンの **[管理]** グループから **[サイト コレクション管理者]** コマンドを選択します。 サイト コレクション管理者である場合は、テキスト ボックスに名前が表示されます。 **[サイト コレクション管理者]** コマンドがリボンの [管理] グループに表示されない場合はサイト コレクション管理者ではないため、サイト管理者から適切なアクセス許可を取得する必要があります。

## <a name="server-explorer-nodes"></a>サーバー エクスプローラーのノード
 SharePoint サイトのすべてのコンポーネントは、**サーバー エクスプローラー** のツリー ビューの **[SharePoint 接続]** 下にあるノードで表されます。 たとえば、既定の SharePoint サイトには [ディスカッション] というコンテンツの種類があります。これは、SharePoint サイトの **[ディスカッション]** ページに表示されるディスカッションの種類を表します。 ディスカッション コンテンツの種類には、いくつかのフィールドがあります。 **サーバー エクスプローラー** でこれらのフィールドを表示するには、 **[コンテンツ タイプ]** ノード、 **[ディスカッション]** ノードの順に展開します。 その下には、[本文]、[ディスカッション タイトル]、[タイトル] などのいくつかのフィールド ノードがあります。

## <a name="node-shortcut-menu-commands"></a>ノードのショートカット メニューのコマンド
 各ノードにはショートカット メニューがあり、ノードを右クリックするか、選択して **Shift**+**F10** キーを選択してアクセスします。 ノードのコマンドには、次のようなものがあります。

|コマンド名|説明|
|------------------|-----------------|
|更新|ツリー ビューを更新し、ノードが最後に表示されてから発生した可能性のある変更を反映します。|
|削除|選択したノードをツリー ビューから削除します。 **注:** このコマンドは、 **[SharePoint 接続]** ノード下にある SharePoint 接続でのみ有効です。|
|Properties|**[プロパティ]** ウィンドウで選択したノードに使用できるプロパティを表示します。 プロパティはすべて読み取り専用であり、すべてのノードにプロパティが関連付けられているわけではありません。|
|接続の追加|参照する SharePoint サイトを指定できます。 **[SharePoint 接続]** ノードおよびサブサイト ノードで使用できます。|
|ブラウザーで表示|選択したリストを Web ブラウザーに表示します。 このコマンドは、 **[リストとライブラリ]** に含まれる **[リスト]** ノード以下の一部のリストに使用できます。|

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: SharePoint 接続を追加または削除する](../sharepoint/how-to-add-or-remove-sharepoint-connections.md)|**サーバー エクスプローラー** の **[SharePoint 接続]** ノードに新しい SharePoint サイトを追加するために必要な手順について説明します。|

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
