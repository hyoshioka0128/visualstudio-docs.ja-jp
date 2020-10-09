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
ms.openlocfilehash: 91e32971013d2dfcf0ee2dc901d84681522c7e89
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861648"
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
 [条件付きコンパイル](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/121hztk3(v=vs.84))   
 [条件付きコンパイル変数](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/s59bkzce(v=vs.84))   
 [@cc_on 諸表](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-cc-on)   
 [@if 諸表](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-if)   
 [@set ステートメント](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-set)