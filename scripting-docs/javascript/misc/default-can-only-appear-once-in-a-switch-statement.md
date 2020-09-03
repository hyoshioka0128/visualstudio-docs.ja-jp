---
title: "' default ' は、' switch ' ステートメント | で1回のみ使用できますMicrosoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: 0fdce6a86665b942098e4542dc237bc1ef22ad8a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85815514"
---
# <a name="default-can-only-appear-once-in-a-switch-statement"></a>'default' は 'switch' ステートメントのなかに、一度のみ表示できます。
Switch ステートメント内で **default** ステートメントを複数回使用しようとしました。 既定のケースでは、switch ステートメントの最後の case ステートメント (フォールスルーケース) になります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ステートメントから余分な **既定** の case ステートメントを削除 `switch` します (switch ステートメントでは、既定の case ステートメントを1つだけ使用します)。  
  
## <a name="see-also"></a>関連項目  
 [switch ステートメント](../../javascript/reference/switch-statement-javascript.md)   
 [プログラムフローの制御](../../javascript/controlling-program-flow-javascript.md)   
 [JavaScript の予約語](../../javascript/reference/javascript-reserved-words.md)