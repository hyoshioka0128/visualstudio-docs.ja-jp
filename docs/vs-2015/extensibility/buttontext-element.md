---
title: ButtonText 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ef22471d20df5582fec96c8a685029a1d475a4a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184572"
---
# <a name="buttontext-element"></a>ButtonText 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このフィールドでは、さまざまなメニューに表示されるテキストを指定できます。 既定では、 `ButtonText` 要素はメニューコントローラーに表示されます。 `ButtonText`他のテキストフィールドが空白の場合も、要素が既定値になります。 `ButtonText`他のテキストフィールドが指定されている場合でも、要素を空白にすることはできません。  
  
## <a name="syntax"></a>構文  
  
```  
<ButtonText>My Command</ButtonText>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Strings 要素](../extensibility/strings-element.md)|やなどのテキスト要素をグループ化し `ButtonText` `CommandName` ます。|  
  
## <a name="text-value"></a>テキスト値  
 要素のテキスト値は、 `ButtonText` テキストを表示するメニュー項目、combos、およびその他のユーザーインターフェイス (UI) の要素に対して表示されるテキストを提供します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
