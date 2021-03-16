---
description: このに値を割り当てようとしました。
title: "' This ' | に割り当てることはできません。Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 3c52118ee78b7ecb7efa94dd6d86cc4fb34c7d1f
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571832"
---
# <a name="cannot-assign-to-this"></a>'this' に割り当てることはできません。
**この** に値を割り当てようとしました。 **これ** は、 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 次のいずれかを参照するキーワードです。

- メソッドを現在実行しているオブジェクト。

- 現在のメソッドが存在しない場合 (またはメソッドが他のオブジェクトに属していない場合) は、グローバルオブジェクト。

メソッドは、 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] オブジェクトを介して呼び出される関数です。 メソッドの内部では、 **この** キーワードは、メソッドが呼び出されたオブジェクトへの参照です ( **新しい** 演算子でクラスコンストラクターを呼び出すことによって作成されたオブジェクトになります)。

メソッド内では、 **これ** を使用して現在のオブジェクトを参照できますが、 **この** に新しい値を割り当てることはできません。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **この** への割り当てを試行しないでください。 インスタンス化されたオブジェクトのプロパティまたはメソッドにアクセスするには、ドット演算子 (例: **circle. radius**) を使用します。

  > [!NOTE]
  > ユーザーが作成した変数に名前を指定する **ことはでき** ません。これは [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 予約語です。

## <a name="see-also"></a>関連項目

- [このステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Operators/this)
- [スクリプトのトラブルシューティング](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/What_went_wrong)
