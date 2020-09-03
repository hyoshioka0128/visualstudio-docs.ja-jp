---
title: "' Break ' をループの外側に設定することはできません |Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT1019
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 11d02172-2a78-4705-a730-d21111db5f42
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0959bad452d3b24ca1475b66e37fbdab1e9c3e7f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85817659"
---
# <a name="cant-have-break-outside-of-loop"></a>'break' をループの外に設定できません。
ループの外側で **break** キーワードを使用しようとしました。 **Break**キーワードは、ループまたはステートメントを終了するために使用され `switch` ます。 ループまたはステートメントの本体に埋め込まれている必要があり `switch` ます。 ただし、 **ラベル** は break キーワードに従うことができます。  
  
```js
break labelname;  
```  
  
 入れ子になったループまたはステートメント**break**を使用 `switch` しており、最も内側ではないループから抜ける必要がある場合は、break キーワードのラベル付き形式のみが必要です。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **Break**キーワードが外側のループまたは switch ステートメントの内側にあることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [break ステートメント](../../javascript/reference/break-statement-javascript.md)   
 [プログラムフローの制御](../../javascript/controlling-program-flow-javascript.md)   
 [スクリプトのトラブルシューティング](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)