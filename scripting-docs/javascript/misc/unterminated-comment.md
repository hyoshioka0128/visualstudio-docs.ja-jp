---
title: 未終了のコメント |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1016
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d4286315-814b-4966-b4c4-1ee19d796eff
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8453b05d2d09537f381bd2947dccb6b0a19a6263
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861844"
---
# <a name="unterminated-comment"></a>未終了のコメントです。
複数行のコメントブロックを開始しましたが、正しく終了しませんでした。 複数行のコメントは "/*" の組み合わせで始まり、逆の "/" の組み合わせで終了し \* ます。 次に例を示します。  
  
```JavaScript  
/* This is a comment  
This is another part of the same comment.*/  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 複数行のコメントは、必ず "*/" で終了してください。  
  
## <a name="see-also"></a>関連項目  
 [コメント ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Lexical_grammar)