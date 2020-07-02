---
title: 無効な置換関数 argument |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4727186f-facd-4aa6-9447-bbefbae83f07
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 452af60c37e4a56996438cc2957e9b69ccee98ef
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816827"
---
# <a name="invalid-replacer-argument"></a>置換関数の引数が無効です。
無効な引数を使用してを呼び出そうとしました `JSON.stringify` 。 引数は、 `replacer` 関数または配列である必要があります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `replacer`関数または配列に引数を変更します。  
  
## <a name="example"></a>例  
 この例のコードで `memberfilter` は、が関数または配列ではなくオブジェクトであるため、ランタイムエラーが発生します。  
  
```JavaScript  
var contact = new Object();  
contact.firstname = "Jesper";  
contact.surname = "Aaberg";  
contact.phone = ["555-0100", "555-0120"];  
  
var memberfilter = new Object();  
  
// This line will cause a runtime error.  
var jsontext = JSON.stringify(contact, memberfilter, "\t");  
```  
  
## <a name="see-also"></a>関連項目  
 [JSON オブジェクト](../../javascript/reference/json-object-javascript.md)   
 [JSON. parse 関数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript ランタイム エラー](../../javascript/reference/javascript-run-time-errors.md)