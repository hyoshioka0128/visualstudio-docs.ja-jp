---
title: Value 引数の循環参照はサポートされていません |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: aa753a4ba3e0254ed7de026653759bbdcfce0631
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862322"
---
# <a name="circular-reference-in-value-argument-not-supported"></a>value 引数の循環参照はサポートされません。
無効な値を使用してを呼び出そうとしました `JSON.stringify` 。 `value`引数 (配列またはオブジェクト) に循環参照が含まれています。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 引数から循環参照を削除します。  
  
## <a name="example"></a>例  
 この例のコードで `john` は、にが参照さ `mary` れ、 `mary` への参照があるため、ランタイムエラーが発生し `john` ます。 循環参照を削除するには、オブジェクトからプロパティを削除するか、オブジェクトからプロパティを設定解除し `brother` `mary` `sister` `john` ます。  
  
```JavaScript  
var john = new Object();  
var mary = new Object();  
john.sister = mary;  
mary.brother = john;  
  
// This line causes a runtime error.  
var error = JSON.stringify(john);  
```  
  
## <a name="see-also"></a>関連項目  
 [JSON オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON)   
 [JSON. parse 関数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)   
 [JavaScript ランタイム エラー](/microsoft-edge/devtools-guide/console/error-and-status-codes#javascript-run-time-errors)