---
title: 正規表現 (JavaScript) では ') ' が必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5020
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 2087ba1d-9783-4d40-b609-e8542f579f7f
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7c10449df9ef3331949695b7423da3eb08b65433
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577537"
---
# <a name="expected--in-regular-expression-javascript"></a>正規表現の中に ')' が必要です (JavaScript)
正規表現のキャプチャ、アサーション、またはグループを作成しようとしましたが、終わりかっこが含まれていませんでした。 正規表現では、かっこにいくつかの目的があります。 主に、サブ式をキャプチャしたり、アサーションを指定したり、パターンをグループ化して、項目を *、+、? などの1つの単位として処理できるようにするために使用されます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 右端の右かっこを追加します。  
  
    > [!NOTE]
    > 1つのかっこに一致させる場合は、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]によって特殊文字として解釈されないように、円記号 (-\\) でエスケープします。  
  
## <a name="see-also"></a>参照  
 [正規表現オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)  
 [正規表現の構文 (JavaScript)](https://msdn.microsoft.com/library/1400241x)
