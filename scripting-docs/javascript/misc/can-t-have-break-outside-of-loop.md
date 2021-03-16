---
description: ループの外側で break キーワードを使用しようとしました。
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
ms.openlocfilehash: d761a1cff89f650e5fc465b6a6aef2713aafb765
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103570649"
---
# <a name="cant-have-break-outside-of-loop"></a>'break' をループの外に設定できません。
ループの外側で **break** キーワードを使用しようとしました。 **Break** キーワードは、ループまたはステートメントを終了するために使用され `switch` ます。 ループまたはステートメントの本体に埋め込まれている必要があり `switch` ます。 ただし、 **ラベル** は break キーワードに従うことができます。  
  
```js
break labelname;  
```  
  
 入れ子になったループまたはステートメントを使用 `switch` しており、最も内側ではないループから抜ける必要がある場合は、break キーワードのラベル付き形式のみが必要です。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **Break** キーワードが外側のループまたは switch ステートメントの内側にあることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [break ステートメント](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/break)   
 [プログラムフローの制御](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)   
 [スクリプトのトラブルシューティング](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/What_went_wrong)
