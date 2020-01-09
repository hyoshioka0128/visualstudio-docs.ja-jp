---
title: "' Break ' をループの外側に設定することはできません |Microsoft Docs"
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 356e7022f940e696030b0cda4f71a599c147dd5a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576015"
---
# <a name="cant-have-break-outside-of-loop"></a>'break' をループの外に設定できません。
ループの外側で**break**キーワードを使用しようとしました。 **break**キーワードは、ループまたは `switch` ステートメントを終了するために使用されます。 ループまたは `switch` ステートメントの本体に埋め込まれている必要があります。 ただし、**label**は break キーワードに従うことができます。  
  
```js
break labelname;  
```  
  
 入れ子になったループまたは `switch` ステートメントを使用しており、最も内側にないループから分割する必要がある場合は、 **break**キーワードのラベル付き形式のみが必要です。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **break**キーワードが外側のループまたは switch ステートメントの内側にあることを確認します。  
  
## <a name="see-also"></a>参照  
 [break ステートメント](../../javascript/reference/break-statement-javascript.md)   
 [プログラムフローの制御](../../javascript/controlling-program-flow-javascript.md)   
 [スクリプトのトラブルシューティング](../../javascript/advanced/troubleshooting-your-scripts-javascript.md)
