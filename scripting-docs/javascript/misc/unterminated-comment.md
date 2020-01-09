---
title: 未終了のコメントです。 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 22bda5d6baabe8874d7514c137ddbcb3e11eb23b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572524"
---
# <a name="unterminated-comment"></a>未終了のコメントです。
複数行のコメントブロックを開始しましたが、正しく終了しませんでした。 複数行のコメントは "/*" の組み合わせで始まり、"\*/" の逆の組み合わせで終了します。 次に例を示します。  
  
```JavaScript  
/* This is a comment  
This is another part of the same comment.*/  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 複数行のコメントは、必ず "*/" で終了してください。  
  
## <a name="see-also"></a>関連項目  
 [コメント ステートメント](../../javascript/reference/comment-statements-javascript.md)
