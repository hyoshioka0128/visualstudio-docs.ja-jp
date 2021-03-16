---
description: 無効な値を使用して json.stringify を呼び出そうとしました。
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
ms.openlocfilehash: 88e4ead99f8c59a1300d018bff9d3e81b0874b51
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571143"
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
