---
title: Visual Studio の外部でアプリを実行するときにアクセス違反をデバッグする
titleSuffix: ''
description: Just-in-Time デバッガーを使用して、Visual Studio 環境の外部で発生するアクセス違反をデバッグします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.access
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 780a298a-132e-4245-8370-8c82ca27c6c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dd4709807b176806d8a7ca56de4adda8cdfe13ec
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99904320"
---
# <a name="how-can-i-debug-access-violations-when-running-my-program-outside-the-debugger"></a>プログラムの実行中にデバッガーの外部で発生するアクセス違反をデバッグするには

## <a name="problem-description"></a>問題の説明
 プログラムが Visual Studio 環境では正しく動作するのに、Windows オペレーティング システムでスタンドアロンで実行するとアクセス違反が発生します。 どのようにデバッグしたらいいのでしょうか。

## <a name="solution"></a>ソリューション
 [[Just-In-Time デバッグ]](../debugger/just-in-time-debugging-in-visual-studio.md) オプションを設定し、アクセス違反が発生するまでプログラムをスタンドアロンで実行します。 その後、 **[アクセス違反です]** ダイアログ ボックスが表示されたら、 **[キャンセル]** をクリックしてデバッガーを起動します。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)