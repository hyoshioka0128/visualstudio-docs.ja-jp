---
title: 正規表現 (JavaScript) では ') ' が必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: af32127476c83100c0340021428e3abc572ef2f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85815644"
---
# <a name="expected--in-regular-expression-javascript"></a>正規表現の中に ')' が必要です (JavaScript)
正規表現のキャプチャ、アサーション、またはグループを作成しようとしましたが、終わりかっこが含まれていませんでした。 正規表現では、かっこにいくつかの目的があります。 主に、サブ式をキャプチャしたり、アサーションを指定したり、パターンをグループ化して、項目を *、+、? などの1つの単位として処理できるようにするために使用されます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 右端の右かっこを追加します。  
  
    > [!NOTE]
    > 1つのかっこに一致させる場合は、円記号 \\ (-) でエスケープします。これは、によって特殊文字として解釈されないようにするため [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] です。  
  
## <a name="see-also"></a>関連項目  
 [正規表現オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)   
 [正規表現の構文 (JavaScript)](https://msdn.microsoft.com/library/1400241x)