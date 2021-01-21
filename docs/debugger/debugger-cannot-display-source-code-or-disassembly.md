---
title: デバッガーでソース コードまたは逆アセンブリを表示できません
description: '[デバッガーは、プログラムの実行が停止したソースコードまたは逆アセンブルを表示できません] メッセージの理由を確認します。'
ms.custom: SEO-VS-2020, seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- disassembly code, errors
ms.assetid: 112d3ea3-fdd2-4bce-92b4-167a76258934
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dd0ed9a798c29010911a1537c99f30ba44e01aea
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96561046"
---
# <a name="debugger-cannot-display-source-code-or-disassembly"></a>[デバッガーは、ソース コードまたは逆アセンブリを表示できません] ダイアログ ボックス
このエラーには、次のメッセージが表示されます。

 デバッガーは、プログラムの実行が停止したソースコードまたは逆アセンブルを表示できません。

 このエラー メッセージは、次のいくつかの理由によって発生します。

- 逆アセンブリをサポートしない言語のデバッグ中に、ソース コードがない場所にあるブレークポイントにヒットした可能性があります。 **[ブレークポイント]** ウィンドウを開き、ブレークポイントを検索して削除します。

- スクリプトをデバッグしている場合は、プログラムにスレッドが存在しないときにブレークポイントにヒットした可能性があります。 **[デバッグ]** メニューの **[ステップ]** または **[続行]** をクリックしてデバッグを再開します。

- セキュリティ上の考慮から、デバッガーが、スタック、スレッド、レジスタ、またはその他のコンテキスト情報をデバッグ中のプログラムから読み取れない可能性があります。 これは、Web アプリケーションをデバッグしていて、仮想ディレクトリの適切なアクセス権がない場合によく発生します。 仮想ディレクトリのセキュリティを匿名に設定して再試行します。

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)