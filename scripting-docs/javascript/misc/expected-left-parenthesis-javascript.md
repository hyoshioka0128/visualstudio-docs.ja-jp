---
title: "' (' (JavaScript) | が必要です。Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1005
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 712315e1-4c68-4f66-84c2-41b83c42d85a
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: adcabbe0b1d7ca7d0298202b5242049b86f8229a
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817100"
---
# <a name="expected--javascript"></a>'(' が必要です。(JavaScript)
かっこのセット内で式を囲みましたが、左中かっこが含まれていませんでした。 一部の式は、始めかっこと終わりかっこのセット内で囲む必要があります。 次の例では、かっこの使用に注意してください。  
  
```JavaScript  
for (initialize; test; increment) {  
statement;  
}  
```  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 評価式に左かっこを追加します。