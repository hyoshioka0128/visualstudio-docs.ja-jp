---
title: MoreInfoURL 要素 (VSIX 言語パックスキーマ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 3f07b67b-95c5-4ae8-8b7e-d643cbbb0348
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c583d67e1920080f11158a4001e191e93e234006
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284401"
---
# <a name="moreinfourl-element-vsix-language-pack-schema"></a>MoreInfoURL 要素 (VSIX 言語パックのスキーマ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

省略可能。 拡張機能に関するローカライズされた情報へのリンク。  
  
## <a name="syntax"></a>構文  
  
```  
<MoreInfoURL>URL</MoreInfoURL>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|なし||  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|なし||  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[VSIX LanguagePack 要素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)|必須です。 VSIX 言語パックのルート要素を提供します。|  
  
## <a name="text-value"></a>テキスト値  
 省略可能。 Web サイトへのリンク。 リンクはテキスト文字列です。  
  
## <a name="element-information"></a>要素情報  
  
|                 |                                                           |
|-----------------|-----------------------------------------------------------|
|    名前空間    | `http://schemas.microsoft.com/developer/vsx-schema-lp/2010` |
|   スキーマ名   |                 VSIX 言語パックのスキーマ                 |
| 検証ファイル |                VSIXLanguagePackSchema                 |
|  空にすることができます   |                      該当なし                       |
  
## <a name="see-also"></a>参照  
 [VSX Language Pack スキーマリファレンス](../extensibility/vsx-language-pack-schema-reference.md)   
 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)   
 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
