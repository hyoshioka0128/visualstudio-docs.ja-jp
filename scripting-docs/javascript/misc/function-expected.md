---
title: 関数が必要です |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5002
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f62ade94-9f6f-4832-9b9b-49a06a385bbe
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f177bf81a43c45dcff4cef3040c64425ed544057
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816970"
---
# <a name="function-expected"></a>関数が必要です。
オブジェクトではなかったオブジェクトに対して **関数プロトタイプ** メソッドのいずれかを呼び出そうとしたか `Function` 、または関数呼び出しコンテキストでオブジェクトを使用しました。 たとえば、次のコードでは、 **例** が関数ではないため、このエラーが生成されます。  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- オブジェクトに対して **関数プロトタイプ** メソッドのみを呼び出し `Function` ます。  
  
- 関数呼び出し演算子を使用して `()` 関数だけを呼び出すようにしてください。  
  
## <a name="see-also"></a>関連項目  
 [関数オブジェクト](../../javascript/reference/function-object-javascript.md)   
 [prototype プロパティ (Object)](../../javascript/reference/prototype-property-object-javascript.md)