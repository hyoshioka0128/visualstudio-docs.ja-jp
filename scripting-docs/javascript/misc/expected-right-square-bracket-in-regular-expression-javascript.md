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
ms.openlocfilehash: 8a2a2b83b818e37c0b62e103fe284c5c4d110c6c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85815632"
---
# <a name="expected--in-regular-expression-javascript"></a>正規表現の中に ']' が必要です (JavaScript)
正規表現と一致する文字クラスを作成しようとしましたが、右かっこが含まれていませんでした。 個々のリテラル文字の組み合わせは、角かっこ内に配置することによって、文字クラスに組み立てることができます。 文字クラスは、それに含まれる任意の1文字と一致します。 たとえば、/[abc]/は、"a"、"b"、または "c" のいずれかの文字と一致します。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 正規表現に右角かっこを追加します。  
  
    > [!NOTE]
    > 1つの角かっこに一致させる場合は、円記号 (-) でエスケープし \\ ます。これは、によって特殊文字として解釈されないようにするため [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] です。  
  
## <a name="see-also"></a>関連項目  
 [正規表現オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)   
 [正規表現の構文 (JavaScript)](https://msdn.microsoft.com/library/1400241x)