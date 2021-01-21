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
ms.openlocfilehash: b49b5cfe7076a4a9504500a63f4d47d2f54bcc1a
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862789"
---
# <a name="default-can-only-appear-once-in-a-switch-statement"></a>'default' は 'switch' ステートメントのなかに、一度のみ表示できます。
Switch ステートメント内で **default** ステートメントを複数回使用しようとしました。 既定のケースでは、switch ステートメントの最後の case ステートメント (フォールスルーケース) になります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ステートメントから余分な **既定** の case ステートメントを削除 `switch` します (switch ステートメントでは、既定の case ステートメントを1つだけ使用します)。  
  
## <a name="see-also"></a>関連項目  
 [switch ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/switch)   
 [プログラムフローの制御](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)   
 [JavaScript の予約語](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Lexical_grammar)