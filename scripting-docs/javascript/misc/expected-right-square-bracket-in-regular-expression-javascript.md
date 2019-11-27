---
title: 正規表現では '] ' が必要です (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 9af38a5fa754a811416f1a998b90946345f3e4a2
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576490"
---
# <a name="expected--in-regular-expression-javascript"></a>正規表現の中に ']' が必要です (JavaScript)
正規表現と一致する文字クラスを作成しようとしましたが、右かっこが含まれていませんでした。 個々のリテラル文字の組み合わせは、角かっこ内に配置することによって、文字クラスに組み立てることができます。 文字クラスは、それに含まれる任意の1文字と一致します。 たとえば、/[abc]/は、"a"、"b"、または "c" のいずれかの文字と一致します。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 正規表現に右角かっこを追加します。  
  
    > [!NOTE]
    > 1つの角かっこに一致させる場合は、円記号 (-) でエスケープ \\[-[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]によって特殊文字として解釈されません。  
  
## <a name="see-also"></a>参照  
 [正規表現オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)の   
 [正規表現の構文 (JavaScript)](https://msdn.microsoft.com/library/1400241x)