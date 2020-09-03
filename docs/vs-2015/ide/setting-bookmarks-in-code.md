---
title: コードへのブックマークの設定 | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.BookmarkWindow
ms.assetid: a752ed5f-5cf9-4bf2-865a-2131ca600ed5
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ba9f9b605d4f82f5244dbc68fb37f96d8ccce51d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673168"
---
# <a name="setting-bookmarks-in-code"></a>コードへのブックマークの設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ブックマークを使用してコード内の行に印を付けると、特定の位置にすぐに戻り、印を付けた位置の間をすばやく移動することができます。

 ブックマークのコマンドとアイコンは、ブックマーク ウィンドウ (**[表示]/[ブックマーク ウィンドウ]**) と [テキスト エディター] ツール バーの 2 か所で使用できます。

## <a name="managing-bookmarks"></a>ブックマークの管理
 ブックマークを追加するには、ブックマークを設定する行にカーソルを置きます。 **トグル** ボタンをクリックするか、Ctrl + K キーを押します。 これで、ブックマークが追加されます。 もう一度、トグル ボタンをクリックすると (または Ctrl + K を押すと)、ブックマークが削除されます。 ブックマーク ウィンドウの **[削除]** ボタンをクリックしても、ブックマークを削除できます。

> [!IMPORTANT]
> ブックマークは、コードではなく行番号に設定されます。 コードを変更しても、ブックマークはその行番号の位置に維持され、コードと一緒に移動しません。

 ブックマーク ウィンドウの **[次のブックマーク]** および **[前のブックマーク]** ボタンを使用して、ブックマークの間で移動できます。

 ブックマーク ウィンドウの **[新しいフォルダー]** をクリックし、選択したブックマークを新しいフォルダーにドラッグして、ブックマークを仮想フォルダーに編成することができます。

 ブックマーク ウィンドウの **[すべてのブックマークを無効にする]** ボタンをクリックして、ブックマークを (削除せずに) オフにできます。 同じボタン (**[すべてのブックマークを有効にする]** に変わっています) をクリックして、ブックマークを再び有効にすることができます。
