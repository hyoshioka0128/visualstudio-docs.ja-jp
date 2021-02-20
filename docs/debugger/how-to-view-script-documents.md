---
title: スクリプト ドキュメントを表示する | Microsoft Docs
description: ソリューション エクスプローラーを使用して Visual Studio で JavaScript のサーバー側スクリプト ドキュメントを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/05/2019
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cfaa4e2558d8d1f102b0e442e9c509313f860e4b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99853099"
---
# <a name="how-to-view-script-documents-javascript"></a>方法: スクリプト ドキュメントを表示する (JavaScript)

サーバー側スクリプト ファイルはソリューション エクスプローラーに表示されます。 クライアント側スクリプト ファイルは、デバッグ モードまたは中断モードのときにのみ表示されます。 クライアント側スクリプト ファイルは、 **[スクリプト ドキュメント]** ノードに表示されます。

ページを動的に生成する一部の種類のアプリケーションでは、ブラウザーに読み込まれるスクリプト ドキュメントからブレークポイントを設定すると、ブレーク モードへの移行とデバッグが簡単になります。 同様に、読み込まれたスクリプト ドキュメントから `debugger` ステートメントを追加して、ブレーク モードにすることができます。 この記事では、これらのドキュメントの表示方法について説明します。

> [!NOTE]
> [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] までは、サーバー側スクリプトによって生成されたクライアント側スクリプト ファイルは [スクリプト エクスプローラー] ウィンドウに表示されました。

### <a name="to-view-a-server-side-script-document"></a>サーバー側スクリプト ドキュメントを表示するには

1. **ソリューション エクスプローラー** で、 **\<Website Pathname>** ノードを開きます。

2. 表示するスクリプト ファイルをダブルクリックします。

     サーバー側スクリプト ファイルがソース ウィンドウに表示されます。

### <a name="to-view-a-client-side-script-document"></a>クライアント側スクリプト ドキュメントを表示するには

1. **ソリューション エクスプローラー** で、 **[スクリプト ドキュメント]** ノードを開きます。

2. 表示するスクリプト ファイルをダブルクリックします。

     クライアント側スクリプト ファイルがソース ウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)