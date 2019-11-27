---
title: 無効な置換関数 argument |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 9ba76a2121dfb3853e38bacbdf49c985103c2a35
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573810"
---
# <a name="invalid-replacer-argument"></a>置換関数の引数が無効です。
無効な引数を使用して `JSON.stringify` を呼び出そうとしました。 `replacer` 引数は、関数または配列である必要があります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `replacer` 引数を関数または配列に変更します。  
  
## <a name="example"></a>例  
 この例のコードでは、`memberfilter` が関数または配列ではなくオブジェクトであるため、ランタイムエラーが発生します。  
  
```JavaScript  
var contact = new Object();  
contact.firstname = "Jesper";  
contact.surname = "Aaberg";  
contact.phone = ["555-0100", "555-0120"];  
  
var memberfilter = new Object();  
  
// This line will cause a runtime error.  
var jsontext = JSON.stringify(contact, memberfilter, "\t");  
```  
  
## <a name="see-also"></a>参照  
 [JSON オブジェクト](../../javascript/reference/json-object-javascript.md)の   
 [JSON. Parse 関数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript ランタイム エラー](../../javascript/reference/javascript-run-time-errors.md)