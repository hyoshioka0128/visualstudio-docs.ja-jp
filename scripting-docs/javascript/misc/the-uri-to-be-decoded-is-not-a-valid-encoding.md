---
title: デコードする URI が有効な encoding | ではありません。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5025
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 029e0790-ffd1-496d-8700-3b3dbac1b6fd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 99df8739137971e32c14f265460ff3f4a9c03816
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572255"
---
# <a name="the-uri-to-be-decoded-is-not-a-valid-encoding"></a>デコードする URI は正しくエンコードされていません。
不適切な形式の URI (Uniform Resource Identifier) をデコードしようとしました。 Uri には特殊な構文があります。URI で使用する前に、ほとんどの英数字以外の文字をエンコードする必要があります。 `encodeURI` および `encodeURIComponent` メソッドを使用して、通常の [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 文字列から URI を作成できます。  
  
 完全な URI は、一連のコンポーネントと区切り記号で構成されます。 一般的な形式は次のとおりです。  
  
```JavaScript  
<Scheme>:<first>/<second>;<third>?<fourth>  
```  
  
 山かっこで囲まれた名前はコンポーネントを表し、":"、"/"、";"、および "?" は、区切り記号として使用される予約文字です。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 有効な Uri のみをデコードしようとしていることを確認します。 無効な文字が含まれている可能性があるため、通常の [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 文字列をデコードすることはできません。  
  
## <a name="see-also"></a>参照  
 [decodeURI 関数](../../javascript/reference/decodeuri-function-javascript.md)   
 [decodeURIComponent 関数](../../javascript/reference/decodeuricomponent-function-javascript.md)
