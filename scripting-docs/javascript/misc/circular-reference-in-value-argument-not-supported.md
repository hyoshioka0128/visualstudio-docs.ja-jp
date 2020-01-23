---
title: Value 引数の循環参照はサポートされていません |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5034
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d06f0fa-86f5-49d1-8d50-af1759990f43
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 542fca58778a7b85b3044ce984b6ea049db12509
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572335"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>value 引数の循環参照はサポートされません。
無効な値を使用して `JSON.stringify` を呼び出そうとしました。 `value` 引数 (配列またはオブジェクト) に循環参照が含まれています。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 引数から循環参照を削除します。  
  
## <a name="example"></a>例  
 この例のコードでは、`john` に `mary` への参照があり、`mary` に `john`への参照が含まれているため、ランタイムエラーが発生します。 循環参照を削除するには、プロパティ `brother` を `mary` オブジェクトから削除するか、または `john` オブジェクトの `sister` プロパティから設定解除します。  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>参照  
 [JSON オブジェクト](../../javascript/reference/json-object-javascript.md)   
 [JSON. Parse 関数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript ランタイム エラー](../../javascript/reference/javascript-run-time-errors.md)
