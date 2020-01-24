---
title: "' return ' ステートメントが関数の外にあります |Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: a90af6de8e2c238e3660111b19d13c1eaf628c9e
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573684"
---
# <a name="return-statement-outside-of-function"></a>'return' ステートメントが関数の外にあります。
コードのグローバルスコープで `return` ステートメントを使用しています。 `return` ステートメントは、関数の本体内でのみ表示されます。  
  
 `()` 演算子を使用した関数の呼び出しは、式です。 すべての式には値があります。`return` ステートメントは、関数によって返される値を指定するために使用されます。 一般的な形式は次のとおりです。  
  
```js
  
return [ expression ];  
```  
  
 `return` ステートメントが実行されると、*式*が評価され、関数の値として返されます。 式が存在しない場合は、 **undefined**が返されます。  
  
 関数本体に他のステートメントが残っている場合でも、関数の実行は、`return` ステートメントの実行時に停止します。 このルールの例外は、 **return**ステートメントが**try**ブロック内に発生し、対応する**finally**ブロックがある場合に、 **finally**ブロック内のコードが関数が返される前に実行されることです。  
  
 関数が `return` ステートメントを実行せずに関数本体の末尾に到達したためにが返された場合、返される値は**未定義**の値です (つまり、関数の結果を大きな式の一部として使用することはできません)。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- コードの本体 (グローバルスコープ) から `return` ステートメントを削除します。  
  
## <a name="see-also"></a>参照  
 [return ステートメント](../../javascript/reference/return-statement-javascript.md)   
 [関数オブジェクト](../../javascript/reference/function-object-javascript.md)   
 [caller プロパティ (Function)](../../javascript/reference/caller-property-function-javascript.md)