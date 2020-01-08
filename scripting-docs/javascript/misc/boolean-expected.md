---
title: ブール値が必要です。 | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 91ff0ec8cbd6e5cedb5ec02a8c574ff137b1c6ad
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576059"
---
# <a name="boolean-expected"></a>ブール値が必要です。
`Boolean` 型以外のオブジェクトで、**Boolean.prototype.toString** メソッドまたは **Boolean.prototype.valueOf**メソッドを呼び出しました。この場合の呼び出し元のオブジェクトは、`Boolean` 型である必要があります。 (例:

```JavaScript
var o = new Object;
o.f = Boolean.prototype.toString;
o.f();
```

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **Boolean.prototype.toString** メソッドまたは **Boolean.prototype.valueOf** メソッドの呼び出しは、**Boolean** 型のオブジェクトでだけ行います。

## <a name="see-also"></a>関連項目

- [Boolean オブジェクト](../../javascript/reference/boolean-object-javascript.md)
- [データの種類](../../javascript/data-types-javascript.md)
- [プログラム フローの制御](../../javascript/controlling-program-flow-javascript.md)
- [データのコピー、受け渡し、および比較](../../javascript/advanced/copying-passing-and-comparing-data-javascript.md)
