---
description: 正しくない形式の URI をデコードしようとしました。
title: デコードする URI が有効な encoding | ではありません。Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
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
ms.openlocfilehash: db9d2f89a193ca4542ff5d1ca5ed5c2ae6419f53
ms.sourcegitcommit: 691d2a47f92f991241fdb132a82c53a537198d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2021
ms.locfileid: "103571988"
---
# <a name="the-uri-to-be-decoded-is-not-a-valid-encoding"></a>デコードする URI は正しくエンコードされていません。
不適切な形式の URI (Uniform Resource Identifier) をデコードしようとしました。 Uri には特殊な構文があります。URI で使用する前に、ほとんどの英数字以外の文字をエンコードする必要があります。 `encodeURI`メソッドとメソッドを使用して、 `encodeURIComponent` 通常の文字列から URI を作成でき [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] ます。  
  
 完全な URI は、一連のコンポーネントと区切り記号で構成されます。 一般的な形式は次のとおりです。  
  
```JavaScript  
<Scheme>:<first>/<second>;<third>?<fourth>  
```  
  
 山かっこで囲まれた名前はコンポーネントを表し、":"、"/"、";"、および "?" は、区切り記号として使用される予約文字です。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 有効な Uri のみをデコードしようとしていることを確認します。 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]無効な文字が含まれている可能性があるため、通常の文字列をデコードすることはできません。  
  
## <a name="see-also"></a>関連項目  
 [decodeURI 関数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/decodeuri)   
 [decodeURIComponent 関数](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/decodeuricomponent)
