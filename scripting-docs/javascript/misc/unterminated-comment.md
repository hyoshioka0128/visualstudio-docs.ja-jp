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
ms.openlocfilehash: 16f675cb62c0c3fd5f3aba7ba6190427fe101353
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85814804"
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
 [コメント ステートメント](../../javascript/reference/comment-statements-javascript.md)