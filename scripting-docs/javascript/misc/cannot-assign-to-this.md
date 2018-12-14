---
title: 'this' に割り当てることはできません。|Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- javascript
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.WebClient.Help.SCRIPT5000
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba2b0a2b-f0f8-4698-b335-a4ab6c166671
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 47e55d39e85675b37d2ac9741d1207a9e81d369e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49856653"
---
# <a name="cannot-assign-to-39this39"></a>'this' に割り当てることはできません。
値を代入しようとしています。**この**します。 **this**は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]キーワードのいずれかを参照します。

- 現在、メソッドを実行するオブジェクト

- 現在のメソッドはありません (または、メソッドが、他のオブジェクトに属していない) 場合は、グローバル オブジェクトです。

メソッドは、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]オブジェクトを介して呼び出される関数。 メソッド内で、**この**キーワードによって、メソッドが呼び出されたオブジェクトへの参照は、(クラスのコンス トラクターを呼び出すことによって作成されたオブジェクトである、**新しい**演算子)。

メソッド内で使用することができます**この**が現在のオブジェクトを参照するために新しい値を割り当てることはできません**この**します。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- 割り当てるしないで**この**します。 プロパティまたはオブジェクトのインスタンスのメソッドにアクセスするには、ドット演算子を使用して (例: **circle.radius**)。

  > [!NOTE]
  > ユーザーが作成した変数の名前を付けられません**この**; は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]予約語。

## <a name="see-also"></a>関連項目

- [this ステートメント](../../javascript/reference/this-statement-javascript.md)
- [スクリプトのトラブルシューティング](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)
