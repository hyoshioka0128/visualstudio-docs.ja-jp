---
title: '[デバッグ操作を停止しています] ダイアログ ボックス | Microsoft Docs'
description: '[デバッグ操作を停止しています] ダイアログ ボックスを調べます。これは、デバッガーによってデバッグ セッションを停止しようとしているものの、セッションの停止に時間がかかる場合に表示されます。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.stopnow
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Stop Debugging in Progress dialog box
ms.assetid: ed7ef49d-e25f-4a4d-9396-9bc7b4143117
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ae8cb1935a5f88335411d5284f32267a9a65e4da
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99904977"
---
# <a name="stop-debugging-in-progress-dialog-box"></a>[デバッグ操作を停止しています] ダイアログ ボックス
このダイアログ ボックスは、デバッガーがデバッグ セッションを停止しようとしているものの、セッションの停止に時間がかかる場合に表示されます。 デバッグ セッションの停止は通常、非常に速く行われ、このダイアログ ボックスは表示されません。 ただし、デバッグ中のすべてのプロセスからデタッチするのに余分な時間がかかることがあります。 セッションの停止に数分以上かかる場合 (またはデタッチ エラーが発生した場合) は、このダイアログ ボックスが表示されます。 この症状が頻繁に発生する場合は、内部に問題がある可能性があります。製品サポート サービスにお問い合わせください。

 プロセスがデタッチし、このダイアログ ボックスが消えるのを待つか、 **[今すぐ停止]** を使って強制的に即時終了します。

 **[今すぐ停止]** : デバッグ セッションをすぐに終了する場合は、このボタンをクリックします。 **[今すぐ停止]** を使用すると、デバッグ中のプロセスのデタッチではなく、デバッグ セッションの終了が行われます。 システム プロセスをデバッグしている場合は、これらのプロセスを **[今すぐ停止]** で終了すると、予想不可能な結果や望ましくない結果になることがあります。

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [プログラムのデタッチ](/previous-versions/visualstudio/visual-studio-2010/x1thkxez(v=vs.100))