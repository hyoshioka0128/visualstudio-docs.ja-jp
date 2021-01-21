---
title: Throw の後には、同じソース行 | の式を指定しなければなりません。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b03b7747-01a1-40c6-af80-a1dd70bc5781
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b1ce004eb523497b912e8d7ec29c3b03044f0220
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91861991"
---
# <a name="throw-must-be-followed-by-an-expression-on-the-same-source-line"></a>Throw ステートメントに指定する式は、ソース コードの同一行に記述してください
`throw`キーワードを使用しましたが、同じソース行で式を使用していませんでした。 ステートメントは、 `throw` キーワードと、その `throw` 後にスローされる式の2つの部分で構成されます。 次に例を示します。  
  
```JavaScript  
if (denominator == 0) {  
 throw new DivideByZeroException();  
}  
```  
  
 これら2つのコンポーネントを分割することはできません。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `throw`キーワードとスローされる式が同じ行に表示されていることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Error オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Error)   
 [throw ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/throw)   
 [お試しください...キャッチ...finally ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/try...catch)