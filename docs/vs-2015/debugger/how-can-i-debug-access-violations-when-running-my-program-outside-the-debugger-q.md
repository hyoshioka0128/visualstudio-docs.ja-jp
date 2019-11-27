---
title: プログラムの実行中にデバッガーの外部で発生するアクセス違反をデバッグするには | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.access
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 780a298a-132e-4245-8370-8c82ca27c6c1
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ce5b21f92eecf2e8929c142bc1ee32e20d386335
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299256"
---
# <a name="how-can-i-debug-access-violations-when-running-my-program-outside-the-debugger"></a>プログラムの実行中にデバッガーの外部で発生するアクセス違反をデバッグするには
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

問題の説明  
 プログラムが Visual Studio 環境では正しく動作するのに、Windows オペレーティング システムでスタンドアロンで実行するとアクセス違反が発生します。 どのようにデバッグしたらいいのでしょうか。  
  
## <a name="solution"></a>解決策:  
 [[Just-In-Time デバッグ]](../debugger/just-in-time-debugging-in-visual-studio.md) オプションを設定し、アクセス違反が発生するまでプログラムをスタンドアロンで実行します。 その後、 **[アクセス違反です]** ダイアログ ボックスが表示されたら、 **[キャンセル]** をクリックしてデバッガーを起動します。  
  
 サポート技術情報の文書「How to Locate Where a General Protection (GP) Fault Occurs (Q133174)」も参照してください。 サポート技術情報の記事については、MSDN ライブラリ CD を参照するか、 [http://support.microsoft.com/](https://support.microsoft.com/)を検索してください。  
  
## <a name="see-also"></a>関連項目  
 [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)   
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
