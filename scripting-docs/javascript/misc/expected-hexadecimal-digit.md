---
description: Unicode エスケープシーケンスが正しく作成されていません。
title: 16進数字 | が必要です。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 67a86df7-49f9-43cb-99c6-99b1a427827a
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 107ce2dd4f9a65a0a04b8e2ec773367ffae4ce81
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570428"
---
# <a name="expected-hexadecimal-digit"></a>16 進数の数字が必要です。
Unicode エスケープシーケンスが正しく作成されていません。 Unicode エスケープシーケンスは、\u で始まり、その後に4桁の16進数が続きます (それ以上はありません)。 Unicode 16 進数には、数字0-9、大文字の A ~ F、および小文字 (a ~ f) のみを含めることができます。 次の例は、正しい形式の Unicode エスケープシーケンスを示しています。  
  
```JavaScript  
z = "\u1A5F";  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- Unicode の16進数は \u で始まり、数字0-9、大文字の A ~ F、小文字 (a ~ f) のみが含まれていることを確認してください。とは4桁にグループ化されています。  
  
    > [!NOTE]
    > 文字列でリテラルテキスト \u を使用する場合は、2つの円記号 (\u) を使用し \\ て、最初の円記号をエスケープします。  
  
## <a name="see-also"></a>関連項目  
 [データの種類](https://developer.mozilla.org/docs/Web/JavaScript/Data_structures)
