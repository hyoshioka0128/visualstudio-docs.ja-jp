---
title: 条件付きコンパイルは無効になっています |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 59a030b0-a6c6-47f2-b90e-c0ed204d5116
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: da272529768f3227ce6e0ee3e0ebbf086140dd15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816125"
---
# <a name="conditional-compilation-is-turned-off"></a>条件付きコンパイルは無効になっています。
条件付きコンパイル変数を使用しようとしましたが、最初に条件付きコンパイルを有効にしませんでした。 条件付きコンパイルを有効に [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] すると、@ で始まる識別子を条件付きコンパイル変数として解釈するようにコンパイラに指示します。 これを行うには、次のステートメントを使用して条件付きコードを開始します。  
  
```js
/*@cc_on @*/  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 条件付きコードの先頭に次のステートメントを追加します。  
  
    ```JavaScript  
    /*@cc_on @*/  
    ```  
  
## <a name="see-also"></a>関連項目  
 [条件付きコンパイル](../../javascript/advanced/conditional-compilation-javascript.md)   
 [条件付きコンパイル変数](../../javascript/advanced/conditional-compilation-variables-javascript.md)   
 [@cc_on 諸表](../../javascript/reference/at-cc-on-statement-javascript.md)   
 [@if 諸表](../../javascript/reference/at-if-statement-javascript.md)   
 [@set ステートメント](../../javascript/reference/at-set-statement-javascript.md)