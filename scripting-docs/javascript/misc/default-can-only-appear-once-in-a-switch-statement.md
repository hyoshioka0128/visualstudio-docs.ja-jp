---
title: "' default ' は、' switch ' ステートメント | で1回のみ使用できますMicrosoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1027
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: a94100f4-6ee5-4759-b635-9d309e47111e
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 90652e44a4bd0362f679be71d0d6401165487aec
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572887"
---
# <a name="default-can-only-appear-once-in-a-switch-statement"></a>'default' は 'switch' ステートメントのなかに、一度のみ表示できます。
switch ステートメントで、**default** ステートメントを複数回使用しようとしました。 default case は、switch ステートメントの最後の case ステートメント (式の値と一致しなかった場合に実行される case) である必要があります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `switch` ステートメントで、**default** case ステートメントを一度だけ使用するようにします (switch ステートメントでは、既定の case ステートメントを 1 つだけ使用します)。  
  
## <a name="see-also"></a>参照  
 [Switch ステートメント](../../javascript/reference/switch-statement-javascript.md)の   
 [プログラムフローの制御](../../javascript/controlling-program-flow-javascript.md)   
 [JavaScript の予約語](../../javascript/reference/javascript-reserved-words.md)