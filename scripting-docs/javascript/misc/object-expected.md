---
description: オブジェクト以外の型のオブジェクトでメソッドまたはプロパティを呼び出そうとしました。または、オブジェクトが必要なときに Object 以外の型の引数を渡しました。
title: オブジェクトが必要です |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5007
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d88c93d-e5b5-4b11-9bb5-bf1a5e41ccc3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a62a68b8dd5289794086dad6858238db6cc4f449
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572066"
---
# <a name="object-expected"></a>オブジェクトが必要です。
`Object` 以外の型のメソッドまたはプロパティを呼び出そうとしたか、または `Object` が必要なときに `Object` 以外の型の引数を渡しました。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Object` 型のオブジェクトに対してのみメソッドまたはプロパティを呼び出します。  
  
- オブジェクト以外の引数でエラーが発生した場合は、`Object` 型のオブジェクトを渡します。  
  
- `Object` 型のオブジェクトの代わりに、未定義または null 参照のどちらが呼び出されているかを調べます。  
  
     たとえば、次のコードの myVar でこのエラーが生じた場合:  
  
    ```JavaScript  
    var str = myVar.toString();  
    ```  
  
     代わりに次のコードを使用できます。  
  
    ```JavaScript  
    if (myVar) {  
        var str = myVar.toString();  
    }  
    ```  
  
## <a name="see-also"></a>関連項目  
 [オブジェクトオブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)   
 [オブジェクトと配列](https://developer.mozilla.org/docs/Learn/JavaScript/Objects)
