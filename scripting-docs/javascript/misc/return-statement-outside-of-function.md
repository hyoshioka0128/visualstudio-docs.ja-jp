---
description: コードのグローバルスコープで return ステートメントを使用しています。
title: "' return ' ステートメントが関数の外にあります |Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 03568f9f-5f4f-4a10-a738-9a73f3832b9e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c275db9b2b13f6730ef62a757502b1d51a59ee43
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571663"
---
# <a name="return-statement-outside-of-function"></a>'return' ステートメントが関数の外にあります。
`return`コードのグローバルスコープでステートメントを使用しています。 ステートメントは、 `return` 関数の本体内でのみ表示されます。  
  
 演算子を使用して関数を呼び出すと `()` 、式になります。 すべての式には値があります。 `return` ステートメントは、関数によって返される値を指定するために使用されます。 一般的な形式は次のとおりです。  
  
```js
  
return [ expression ];  
```  
  
 ステートメントを `return` 実行すると、 *式* が評価され、関数の値として返されます。 式が存在しない場合は、 **undefined** が返されます。  
  
 関数 `return` 本体に他のステートメントが残っている場合でも、関数の実行はステートメントの実行時に停止します。 このルールの例外は、 **return** ステートメントが **try** ブロック内に発生し、対応する **finally** ブロックがある場合に、 **finally** ブロック内のコードが関数が返される前に実行されることです。  
  
 関数がステートメントを実行せずに関数本体の末尾に到達したためにが返された場合 `return` 、返される値は **未定義** の値です (つまり、関数の結果を大きな式の一部として使用することはできません)。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `return`コードの本体 (グローバルスコープ) からステートメントを削除します。  
  
## <a name="see-also"></a>関連項目  
 [return ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/return)   
 [関数オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [caller プロパティ (Function)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function/caller)
