---
title: Date オブジェクトが必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5006
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d6ab82e6-ca64-46b4-a06c-5c6b0aa057cb
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 28531c1ac1dc73ca2bf309d412b08d23dd17bfb8
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862638"
---
# <a name="date-object-expected"></a>データ オブジェクトが必要です。
以外の型のオブジェクトに対して、 **日付の prototype** または **date. prototype** . 値のメソッドを呼び出そうとしまし `Date` た。 この種類の呼び出しのオブジェクトは、型である必要があり `Date` ます。 次に例を示します。  
  
```JavaScript  
var o = new Object;  
o.f = Date.prototype.toString;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 型のオブジェクトに対してのみ、 **日付の prototype** または **日付の prototype** メソッドを呼び出し `Date` ます。  
  
## <a name="see-also"></a>関連項目  
 [Date オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date)   
 [getDate メソッド (Date)](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date/getdate)   
 [組み込みオブジェクト](https://developer.mozilla.org/docs/Learn/JavaScript/Objects)