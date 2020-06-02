---
title: '[デバッグ操作を停止しています] ダイアログ ボックス | Microsoft Docs'
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3beefe16f8883eb64d7d0a2641cabf9eb1f702fa
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729656"
---
# <a name="stop-debugging-in-progress-dialog-box"></a>[デバッグ操作を停止しています] ダイアログ ボックス
このダイアログ ボックスは、デバッガーがデバッグ セッションを停止しようとしているものの、セッションの停止に時間がかかる場合に表示されます。 デバッグ セッションの停止は通常、非常に速く行われ、このダイアログ ボックスは表示されません。 ただし、デバッグ中のすべてのプロセスからデタッチするのに余分な時間がかかることがあります。 セッションの停止に数分以上かかる場合 (またはデタッチ エラーが発生した場合) は、このダイアログ ボックスが表示されます。 この症状が頻繁に発生する場合は、内部に問題がある可能性があります。製品サポート サービスにお問い合わせください。

 プロセスがデタッチし、このダイアログ ボックスが消えるのを待つか、 **[今すぐ停止]** を使って強制的に即時終了します。

 **[今すぐ停止]** : デバッグ セッションをすぐに終了する場合は、このボタンをクリックします。 **[今すぐ停止]** を使用すると、デバッグ中のプロセスのデタッチではなく、デバッグ セッションの終了が行われます。 システム プロセスをデバッグしている場合は、これらのプロセスを **[今すぐ停止]** で終了すると、予想不可能な結果や望ましくない結果になることがあります。

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [プログラムのデタッチ](/previous-versions/visualstudio/visual-studio-2010/x1thkxez(v=vs.100))