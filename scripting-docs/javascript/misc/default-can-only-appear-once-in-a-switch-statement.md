---
description: Switch ステートメント内で default ステートメントを複数回使用しようとしました。
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
ms.openlocfilehash: 346643f1ecaae6ab59c0fa265ffe5ff55fa66dc9
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571065"
---
# <a name="default-can-only-appear-once-in-a-switch-statement"></a>'default' は 'switch' ステートメントのなかに、一度のみ表示できます。
Switch ステートメント内で **default** ステートメントを複数回使用しようとしました。 既定のケースでは、switch ステートメントの最後の case ステートメント (フォールスルーケース) になります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ステートメントから余分な **既定** の case ステートメントを削除 `switch` します (switch ステートメントでは、既定の case ステートメントを1つだけ使用します)。  
  
## <a name="see-also"></a>関連項目  
 [switch ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/switch)   
 [プログラムフローの制御](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)   
 [JavaScript の予約語](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Lexical_grammar)
