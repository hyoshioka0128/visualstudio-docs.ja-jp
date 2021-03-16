---
description: 正規表現の検索パターンを作成するときに、無効な繰り返し要素を含む pattern 要素を作成しました。
title: 予期しない量指定子です (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba6d34f9-2d6f-486c-a929-6cd9818be322
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9351f9306cea9e3f6346b007d6fe05c1d7bbf319
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571962"
---
# <a name="unexpected-quantifier-javascript"></a>予期しない量指定子です (JavaScript)
正規表現の検索パターンを作成するときに、無効な繰り返し要素を含む pattern 要素を作成しました。 たとえば、  
  
```js
/^+/  
```  
  
 は無効です。要素 ^ (入力の先頭) に繰り返し要素を含めることはできません。 次の表に、繰り返し要素を持つことができない要素の一覧を示します。  
  
|要素|説明|  
|-------------|-----------------|  
|^|入力の開始|  
|$|入力の終わり|  
|\b|ワード境界|  
|\B|ワード境界以外|  
|*|0回以上の繰り返し|  
|+|1回以上の繰り返し|  
|?|0回または1回の繰り返し|  
|非該当|n 回の繰り返し|  
|{n,}|n 回以上の繰り返し|  
|{n, m}|N ~ m 回の繰り返し (包含)|  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 検索パターン要素に法的な繰り返し要素のみが含まれていることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [正規表現オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [正規表現の構文 (JavaScript)](/previous-versions/1400241x(v=vs.100))
