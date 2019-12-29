---
title: String が必要です |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5005
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4c214c4b-9cd7-473b-8d90-2344c0375c25
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 06f00cd523d2f42a8602347a77935705bbc25932
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573683"
---
# <a name="string-expected"></a>文字列が必要です。
`String` 型以外のオブジェクトで、**String.prototype.toString** メソッドまたは **String.prototype.valueOf** メソッドを呼び出しました。この場合の呼び出し元のオブジェクトは、`String` 型である必要があります。
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- **String.prototype.toString** メソッドまたは **String.prototype.valueOf** メソッドの呼び出しは、`String` 型のオブジェクトでだけ行います。
  
## <a name="see-also"></a>参照  
 [文字列オブジェクト](../../javascript/reference/string-object-javascript.md)   
 [toString メソッド (Object)](../../javascript/reference/tostring-method-object-javascript.md)
