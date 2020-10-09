---
title: 文字セットの範囲が無効です (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5021
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 971e9d5a-f88a-47a8-af94-f3c7c4aed5ab
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 12624d1a0256360ef1e4538a14100923c7de8af8
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862583"
---
# <a name="invalid-range-in-character-set-javascript"></a>文字セットの範囲が無効です (JavaScript)
無効な文字セットの範囲を使用して正規表現を作成しようとしました。 文字セットは、a ~ z や0-9 のように、単一の文字から指定する必要があります。\w などの文字クラスを文字セットに含めることはできません。 範囲内の最初の文字も、範囲内の2番目の文字の前に指定する必要があります。 次に例を示します。  
  
```JavaScript  
var good = /[a-z]/;     // A valid character range - a comes before z.  
var notGood = /[z-a]/;  // An invalid character range - z does not come before a.  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 正規表現の文字セットを構成するために1つの文字だけを使用し、正しい順序になっていることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [正規表現オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [正規表現の構文 (JavaScript)](/previous-versions/1400241x(v=vs.100))