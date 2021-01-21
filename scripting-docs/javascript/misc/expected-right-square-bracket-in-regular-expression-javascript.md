---
title: 正規表現では '] ' が必要です (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 1ca2079a-44dd-479f-a1e3-e04a14d0739e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 31d1ebd30ba5e793a1c52c00d8b58603bdaa9a75
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862326"
---
# <a name="expected--in-regular-expression-javascript"></a>正規表現の中に ']' が必要です (JavaScript)
正規表現と一致する文字クラスを作成しようとしましたが、右かっこが含まれていませんでした。 個々のリテラル文字の組み合わせは、角かっこ内に配置することによって、文字クラスに組み立てることができます。 文字クラスは、それに含まれる任意の1文字と一致します。 たとえば、/[abc]/は、"a"、"b"、または "c" のいずれかの文字と一致します。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 正規表現に右角かっこを追加します。  
  
    > [!NOTE]
    > 1つの角かっこに一致させる場合は、円記号 (-) でエスケープし \\ ます。これは、によって特殊文字として解釈されないようにするため [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] です。  
  
## <a name="see-also"></a>関連項目  
 [正規表現オブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)   
 [正規表現の構文 (JavaScript)](/previous-versions/1400241x(v=vs.100))