---
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
ms.openlocfilehash: 28eec125914f0207fbdf79a39ea2140dd74d6d0d
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816229"
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
 [オブジェクトオブジェクト](../../javascript/reference/object-object-javascript.md)   
 [オブジェクトと配列](../../javascript/objects-and-arrays-javascript.md)