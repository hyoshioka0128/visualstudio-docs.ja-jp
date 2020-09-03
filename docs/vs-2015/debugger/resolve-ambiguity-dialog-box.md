---
title: '[あいまいさの解決] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.Disambig
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b35d305bbd011adc02692cd7c9c687ac0bfc7d45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148790"
---
# <a name="resolve-ambiguity-dialog-box"></a>[あいまいさの解決] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[`Resolve Ambiguity`] ダイアログ ボックスが表示されるのは、表示する場所をデバッガーが選択できない場合です。 たとえば、C++ テンプレートを使用する場合は、単一の関数テンプレートから複数の関数を作成できます。 デバッガーがテンプレートのソースの場所で停止して、`Go To Disassembly` が選択されている場合、デバッガーには複数のオプションがあります。 テンプレートから作成された各関数は独自の逆アセンブリ コードを持っており、デバッガーはどのコードを表示するのかを認識していません。 [`Resolve Ambiguity`] ダイアログ ボックスでは、対応するすべての場所の一覧から目的の場所を選択できます。  
  
 `Choose the specific location`  
 コマンドに対応するすべての場所の一覧を表示します。  
  
 `Address`  
 各関数のメモリ アドレスを表示します。  
  
 `Function`  
 各関数の名前を表示します。  
  
 `Module`  
 関数のオブジェクト コードを含むモジュール (EXE または DLL) を表示します。  
  
## <a name="see-also"></a>参照  
 [デバッガー内の式](../debugger/expressions-in-the-debugger.md)
