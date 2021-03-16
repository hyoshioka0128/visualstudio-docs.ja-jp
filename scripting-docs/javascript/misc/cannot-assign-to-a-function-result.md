---
description: 関数の結果に値を割り当てようとしました。
title: 関数の結果 | を割り当てることはできません。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5003
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ee8ffb3a-1451-4cb3-99bf-5e9cf8b77d79
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 125d2dc7d41b1b65027952e4e6cb94ff97083e6e
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571923"
---
# <a name="cannot-assign-to-a-function-result"></a>関数の結果に割り当てられません。
関数の結果に値を割り当てようとしました。 関数の結果を変数に代入することはできますが、変数として使用することはできません。 関数自体に新しい値を代入する場合は、かっこ (関数呼び出し演算子) を省略します。 次の例は、このエラーが生成される状況を示しています。  
  
```js
myFunction() = 42;  // Attempting to assign the value 42 to the result of the function call.  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 関数呼び出しの結果の値は、 *割り当て* 可能なものとして使用しないでください。 関数呼び出しの結果を *変数に* 割り当てることができます。  
  
    ```JavaScript  
    myVar = myFunction(42);  
    ```  
  
- または、関数自体 (戻り値ではなく) を変数に代入することもできます。  
  
    ```JavaScript  
    myFunction = new Function("return 42;");  
    ```  
  
## <a name="see-also"></a>関連項目  
 [関数オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Function)   
 [JavaScript コードの記述](https://developer.mozilla.org/docs/Learn/Getting_started_with_the_web/JavaScript_basics)   
 [関数](https://developer.mozilla.org/docs/Learn/JavaScript/Building_blocks/Functions)
