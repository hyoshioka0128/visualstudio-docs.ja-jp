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
ms.openlocfilehash: e8012eb02d143a741cb7eea70c45cabc4ee92002
ms.sourcegitcommit: d9254e54079ae01cdf2d07b11f988faf688f80fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88114298"
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
|[VSIX LanguagePack 要素](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)|必須。 VSIX 言語パックのルート要素を提供します。|  
  
## <a name="text-value"></a>テキスト値  
 省略可能。 Web サイトへのリンク。 リンクはテキスト文字列です。  
  
## <a name="element-information"></a>要素情報  

:::row:::
    :::column:::
        名前空間
    :::column-end:::
    :::column:::
        `http://schemas.microsoft.com/developer/vsx-schema-lp/2010`
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        スキーマ名
    :::column-end:::
    :::column:::
        VSIX 言語パックのスキーマ
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        検証ファイル
    :::column-end:::
    :::column:::
        VSIXLanguagePackSchema
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        空にすることができます
    :::column-end:::
    :::column:::
        適用なし
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [VSX Language Pack スキーマリファレンス](../extensibility/vsx-language-pack-schema-reference.md)   
 [VSIX パッケージのローカライズ](../extensibility/localizing-vsix-packages.md)   
 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
