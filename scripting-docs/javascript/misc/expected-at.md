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
ms.openlocfilehash: 209a8793c0940511b7ecb2abb32f537a614ebf8b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85814825"
---
# <a name="expected-"></a>'\@' が必要です
ステートメントを使用して条件付きコンパイルステートメントで使用する変数を作成しようとしました `@set` が、 **@** 変数名の前にアットマーク "" を配置しませんでした。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 変数名の直前にアットマーク "" を追加 **@** します。 次に例を示します。  
  
    ```JavaScript  
    @set @myvar = 1  
    ```  
  
## <a name="see-also"></a>関連項目  
 [@set 諸表](../../javascript/reference/at-set-statement-javascript.md)   
 [条件付きコンパイル](../../javascript/advanced/conditional-compilation-javascript.md)   
 [条件付きコンパイル変数](../../javascript/advanced/conditional-compilation-variables-javascript.md)
