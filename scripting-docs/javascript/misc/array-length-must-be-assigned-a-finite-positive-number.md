---
title: 配列の長さには、有限の正の数を指定する必要があります |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5030
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: c51c66a4-a543-4e95-b18d-2cfbcb3d1fdd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8e0016c7a0a6acb3f08121d8636ccdf848dcf201
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862808"
---
# <a name="array-length-must-be-assigned-a-finite-positive-number"></a>配列の長さは、割り当てられた有限の正数でなければなりません。
既存の**配列**オブジェクトの**length**プロパティを設定するときに、正の数または0ではない配列の長さを指定しました。 このエラーは、負の値または非数 () のオブジェクトの **length** プロパティに値を代入したときに発生し `Array` `NaN` ます。 は、 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 小数部を整数に自動的に変換することに注意してください。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 長さのプロパティに正の整数を割り当てます。 配列のサイズの上限は、最大の整数値 (約 40億) を超えています。 次の例は、**配列**オブジェクトの**length**プロパティを適切に設定する方法を示しています。  
  
    ```JavaScript  
    var my_array = new Array();  
    my_array.length = 99;  
    ```  
  
## <a name="see-also"></a>関連項目  
 [配列の使用](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/Arrays)