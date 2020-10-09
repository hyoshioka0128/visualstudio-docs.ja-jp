---
title: Enumerator オブジェクトが必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5015
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: dc6e32c1-a6e6-4e12-ac99-e3f65f91c8d7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5e63ee2970c90ffcfff5c02a384d3346b3ea6229
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862630"
---
# <a name="enumerator-object-expected"></a>列挙子オブジェクトが必要です。
以外の型のオブジェクトに対して、 **enumerator** 、enumerator、列挙子、列挙子、または **enumerator** . prototype. プロトタイプのメソッドを呼び出そうとしまし `Enumerator` た。 この種類の呼び出しのオブジェクトは、型である必要があり `Enumerator` ます。 この規則を解除するコードの例を次に示します。  
  
```JavaScript  
var o = new Object;  
o.f = Enumerator.prototype.atEnd;  
o.f();  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 型のオブジェクトに対して**のみ、****列挙子**、プロトタイプ、列挙子、列挙**子、enumerator、また**は**enumerator** . prototype. moveNext メソッドを `Enumerator` 呼び出します。 オブジェクトがオブジェクトであるかどうかを確認するには `Enumerator` 、次のように使用します。  
  
    ```js
    if(x instanceof Enumerator)  
    ```  
  
## <a name="see-also"></a>関連項目  
 [Enumerator オブジェクト](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/Enumerator)