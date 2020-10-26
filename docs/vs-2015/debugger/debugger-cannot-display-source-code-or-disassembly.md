---
title: デバッガーでソースコードまたは逆アセンブリを表示できません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- disassembly code, errors
ms.assetid: 112d3ea3-fdd2-4bce-92b4-167a76258934
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5ce4460aecb634523de02f2e3f6929b206b415e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186504"
---
# <a name="debugger-cannot-display-source-code-or-disassembly"></a>[デバッガーは、ソース コードまたは逆アセンブリを表示できません] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーには、次のメッセージが表示されます。  
  
 デバッガーは、プログラムの実行が停止したソースコードまたは逆アセンブルを表示できません。  
  
 このエラー メッセージは、次のいくつかの理由によって発生します。  
  
- 逆アセンブリをサポートしない言語のデバッグ中に、ソース コードがない場所にあるブレークポイントにヒットした可能性があります。 **[ブレークポイント]** ウィンドウを開き、ブレークポイントを検索して削除します。  
  
- スクリプトをデバッグしている場合は、プログラムにスレッドが存在しないときにブレークポイントにヒットした可能性があります。 **[デバッグ]** メニューの **[ステップ]** または **[続行]** をクリックしてデバッグを再開します。  
  
- セキュリティ上の考慮から、デバッガーが、スタック、スレッド、レジスタ、またはその他のコンテキスト情報をデバッグ中のプログラムから読み取れない可能性があります。 これは、Web アプリケーションをデバッグしていて、仮想ディレクトリの適切なアクセス権がない場合によく発生します。 仮想ディレクトリのセキュリティを匿名に設定して再試行します。  
  
## <a name="see-also"></a>参照  
 [デバッガーの基本](../debugger/debugger-basics.md)   
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)   
 [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
