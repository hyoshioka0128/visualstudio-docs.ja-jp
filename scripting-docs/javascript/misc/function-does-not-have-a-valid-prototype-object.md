---
title: 関数には、有効なプロトタイプ オブジェクトが存在しません。 | Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5023
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: b9e34652-190f-4b57-b253-df2e8c4d09c6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cb3cffa4bffd616560aa95ace4ad82a4368ebbd5
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574604"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>関数には、有効なプロトタイプ オブジェクトが存在しません。
**Instanceof** 演算子を使用して、オブジェクトが特定の関数クラスから派生したかどうかを判断しようとしましたが、オブジェクトの `prototype` プロパティを `null`または外部オブジェクト型 (両方とも有効な [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] オブジェクト) として再定義しました。 外部オブジェクトには、ホストオブジェクトモデル (Internet Explorer のドキュメントまたはウィンドウオブジェクトなど) のオブジェクト、または外部 COM オブジェクトを指定できます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 関数の `prototype` プロパティが有効な [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] オブジェクトを参照するようにします。  
  
## <a name="see-also"></a>参照  
 [Function オブジェクト](../../javascript/reference/function-object-javascript.md)  
 [prototype プロパティ (Object)](../../javascript/reference/prototype-property-object-javascript.md)
