---
title: 関数に有効なプロトタイプオブジェクト | がありません。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: ca6f13620bb486cf1663bd5bef9a9a93b2c8a480
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85817360"
---
# <a name="function-does-not-have-a-valid-prototype-object"></a>関数には、有効なプロトタイプ オブジェクトが存在しません。
**Instanceof**を使用して、オブジェクトが特定の関数クラスから派生したかどうかを判断しようとしましたが、オブジェクトの `prototype` プロパティを `null` または外部オブジェクト型 (両方とも有効なオブジェクト) として再定義しました [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 。 外部オブジェクトには、ホストオブジェクトモデル (Internet Explorer のドキュメントまたはウィンドウオブジェクトなど) のオブジェクト、または外部 COM オブジェクトを指定できます。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 関数のプロパティが `prototype` 有効なオブジェクトを参照していることを確認し [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] ます。  
  
## <a name="see-also"></a>関連項目  
 [関数オブジェクト](../../javascript/reference/function-object-javascript.md)   
 [prototype プロパティ (Object)](../../javascript/reference/prototype-property-object-javascript.md)