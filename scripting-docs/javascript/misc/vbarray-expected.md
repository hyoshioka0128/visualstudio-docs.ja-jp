---
description: Visual Basic safeArray ではなかったオブジェクトが必要なときに指定しました。
title: VBArray が必要です |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5013
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f2998d7d-13a4-4bbe-b872-3ff3316551e4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e344e24b3fbef7b7f119a36513c222e085328072
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103572079"
---
# <a name="vbarray-expected"></a>VBArray が必要です。
Visual Basic safeArray ではなかったオブジェクトが必要なときに指定しました。  
  
```js
new VBArray(safeArray);  
```  
  
 VBArrays は読み取り専用で、直接作成することはできません。 SafeArray 引数は VBArray 値であり、コンストラクターに渡される前に VBArray 値を取得する必要があり `VBArray` ます。 この操作は、既存の ActiveX またはその他のオブジェクトから値を取得することによってのみ行うことができます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **Vbarray コンストラクターに** **vbarray** オブジェクトのみを渡していることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [VBArray オブジェクト](https://developer.mozilla.org/docs/Archive/Web/JavaScript/Microsoft_Extensions/VBArray)   
 [配列の使用](https://developer.mozilla.org/docs/Learn/JavaScript/First_steps/Arrays)
