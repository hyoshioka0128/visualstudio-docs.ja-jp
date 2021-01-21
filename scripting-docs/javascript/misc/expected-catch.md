---
title: "' Catch ' | が必要です。Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1033
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f1cd947f-eba2-411e-8e84-8ca86f608643
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 47411a6376cd843b3a12cf74ed1800775b98cd83
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861952"
---
# <a name="expected-catch"></a>catch が必要です。
例外処理 **try** ブロックを使用しましたが、関連付けられた **catch** ステートメントが書き込まれませんでした。 例外処理機構では、例外が発生した場合に実行してはならないコードと共に、失敗する可能性のあるコードが **try** ブロック内にラップされている必要があります。 例外は、 **throw**ステートメントを使用して**try**ブロック内からスローされ、 **try**ブロックの外側で1つ以上の**catch**ステートメントを使用してキャッチされます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 関連付けられた **catch** ブロックを追加します。  
  
- **Catch**ブロックの代わりに**finally**ブロックを使用してください。  
  
## <a name="see-also"></a>関連項目  
 [お試しください...キャッチ...finally ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)   
 [Error オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)