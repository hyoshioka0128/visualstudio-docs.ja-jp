---
title: "' This ' | に割り当てることはできません。Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5000
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba2b0a2b-f0f8-4698-b335-a4ab6c166671
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 73baa77cc63e3a43ac30e70f66081bbc7ade3020
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572352"
---
# <a name="cannot-assign-to-this"></a>'this' に割り当てることはできません。
**this** に値を割り当てようとしました。 **this** は、次のいずれかを参照する [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] キーワードです。

- メソッドを現在実行しているオブジェクト。

- 現在のメソッドが存在しない場合 (またはメソッドが他のオブジェクトに属していない場合) は、グローバルオブジェクト。

メソッドは、オブジェクトを介して呼び出される [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 関数です。 メソッドの内部では、**this** キーワードは、メソッドが呼び出されたオブジェクトへの参照です (**new** 演算子でクラスコンストラクターを呼び出すことによって作成されたオブジェクトになります)。

メソッド内では、**this** を使用して現在のオブジェクトを参照できますが、**this** に新しい値を割り当てることはできません。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **this** に値を割り当てないようにします。 インスタンス化されたオブジェクトのプロパティまたはメソッドにアクセスするには、ドット演算子(例: **circle. radius**) を使用します。

  > [!NOTE]
  > ユーザーが作成した変数に名前を指定する**ことはでき**ません。[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] の予約語です。

## <a name="see-also"></a>関連項目

- [this ステートメント](../../javascript/reference/this-statement-javascript.md)
- [スクリプトのトラブルシューティング](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)