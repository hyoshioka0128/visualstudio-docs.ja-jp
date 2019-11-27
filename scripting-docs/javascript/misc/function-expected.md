---
title: 関数が必要です |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 988ca00613d3dec4c55309fd77bc43705a6038ae
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576595"
---
# <a name="function-expected"></a>関数が必要です。
`Function` オブジェクトではなかったオブジェクトに対して**関数プロトタイプ**メソッドのいずれかを呼び出そうとしたか、または関数呼び出しコンテキストでオブジェクトを使用しました。 次のコードがこのエラーを生成するため、たとえば、**example**は関数ではありません。  
  
```JavaScript  
var example = new Object();  // Create a new object called "example".  
var x = example();           // Try and call example as if it were a function.  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Function` のオブジェクトに対してのみ**関数プロトタイプ**メソッドを呼び出します。  
  
- 関数呼び出し演算子 `()` を使用して関数だけを呼び出すようにしてください。  
  
## <a name="see-also"></a>参照  
 [関数オブジェクト](../../javascript/reference/function-object-javascript.md)の   
 [prototype プロパティ (Object)](../../javascript/reference/prototype-property-object-javascript.md)
