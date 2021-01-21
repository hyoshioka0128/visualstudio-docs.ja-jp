---
title: ブール値が必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5010
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 35d71b7f-53fd-44c4-a7c7-b1550c65cfd4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b6d88815a33187e209bcba248d3c363afdd91227
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862663"
---
# <a name="boolean-expected"></a>ブール値が必要です。
以外の型のオブジェクトで、Boolean. prototype **. toString**または**boolean. prototype. 値**を呼び出そうとしました。 `Boolean` この種類の呼び出しのオブジェクトは、型である必要があり `Boolean` ます。 次に例を示します。

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **ブール型の**オブジェクトに対してのみ、ブール型の**プロトタイプ**または**ブール**型の値のメソッドを呼び出します。

## <a name="see-also"></a>関連項目

- [Boolean オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [Data Types (データ型)](https://developer.mozilla.org/docs/Web/JavaScript/Data_structures)
- [プログラム フローの制御](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [データのコピー、受け渡し、および比較](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Functions)