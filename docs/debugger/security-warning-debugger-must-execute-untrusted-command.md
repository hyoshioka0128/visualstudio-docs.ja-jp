---
title: セキュリティ警告:デバッガーで信頼されないコマンドを実行する必要があります | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.securityalert
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: e5c004b3-b364-4098-ac98-770076ca9981
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0922461c4ca5366e6d1dc215f5711f5566d00ae
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729752"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>セキュリティ警告:デバッガーは信頼されないコマンドを実行する必要があります
ソース サーバーを使用している場合、この警告ダイアログ ボックスが表示されます。 デバッガーがソース コードを取得するために実行する必要のあるコマンドが、srcsvr.ini ファイルに含まれる、ソース サーバーに対して信頼できるコマンドの一覧に記載されていないことを示します。 このコマンドが有効な場合、srcsvr.ini ファイルに追加できます。 それ以外の場合は、そのコマンドを実行しないようにしてください。 詳細については、[シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事をご覧ください。

## <a name="message-text"></a>メッセージ テキスト
 **ソース サーバーからソースを取得するために、この信頼されていないコマンドを実行します。**

 **既知の信頼できる発信元からのデバッグ シンボル ファイル (\*.pdb) でない場合、コマンドは無効であるか、または実行に危険が伴うおそれがあります。**

 **このコマンドを実行しますか。**

## <a name="uielement-list"></a>UIElement の一覧
 テキスト ボックス: 実行する .pdb ファイルの コマンド。

 実行: コマンドの実行を許可します。

 実行しない: コマンドの実行およびソース サーバーからのファイルのダウンロードを停止します。

## <a name="see-also"></a>関連項目
- [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ソース サーバー](/windows/desktop/Debug/source-server-and-source-indexing)