---
title: 自分のアプリをステップ実行しているときにフォーカスを保持する | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.stepping
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], stepping
- focus, keeping
- stepping, focus
- windows, troubleshooting activation
ms.assetid: 11a30580-3a1a-4be8-a241-0abdc758302e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d41a1bf5f71624751fc94f4a72f06e6da5c39630
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350382"
---
# <a name="how-can-i-keep-focus-when-stepping-through-my-app"></a>自分のアプリをステップ実行しているときにフォーカスを保持するにはどうすればよいですか。
## <a name="description"></a>説明
 プログラムで、ウィンドウのアクティブ化が正しく動作しません。 デバッガーでプログラムをステップ実行すると、プログラムがフォーカスを保持できないため、問題を再現できなくなります。 どのようにすればフォーカスを保持できますか。

## <a name="solution"></a>ソリューション
 コンピューターがもう 1 台ある場合は、リモート デバッグを行います。 リモート コンピューター上でプログラムを操作し、ホスト上でデバッガーを実行します。 詳細については、[リモート コンピューターを選択する](/previous-versions/visualstudio/visual-studio-2010/w8wtw2f3(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)