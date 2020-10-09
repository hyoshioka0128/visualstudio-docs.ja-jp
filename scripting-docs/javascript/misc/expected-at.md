---
title: "' @ ' | が必要です。Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1032
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 82ff8b74-1710-4358-9a26-dc92ab29c53b
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 98a35421054e4d2236fe509224ed146063b61a79
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862312"
---
# <a name="expected-"></a>'\@' が必要です
ステートメントを使用して条件付きコンパイルステートメントで使用する変数を作成しようとしました `@set` が、 **@** 変数名の前にアットマーク "" を配置しませんでした。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 変数名の直前にアットマーク "" を追加 **@** します。 次に例を示します。  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>関連項目  
 [@set 諸表](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/at-set)   
 [条件付きコンパイル](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/121hztk3(v=vs.84))   
 [条件付きコンパイル変数](/previous-versions/windows/internet-explorer/ie-developer/scripting-articles/s59bkzce(v=vs.84))