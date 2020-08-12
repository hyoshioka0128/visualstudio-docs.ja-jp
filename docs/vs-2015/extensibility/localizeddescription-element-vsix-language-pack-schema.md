---
title: LocalizedDescription 要素 (VSIX 言語パックスキーマ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 766a1732-bbaf-4875-b276-feb42169633a
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3b4eb077ba8c957466568967804487929254117e
ms.sourcegitcommit: d9254e54079ae01cdf2d07b11f988faf688f80fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88114194"
---
# <a name="localizeddescription-element-vsix-language-pack-schema"></a>LocalizedDescription 要素 (VSIX 言語パックのスキーマ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必須。 拡張機能のローカライズされた説明を提供します。  
  
## <a name="syntax"></a>構文  
  
```  
<LocalizedDescription>Localized description of the extension</LocalizedDescription>  
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
 必須。 ターゲット言語における拡張機能の説明テキスト。  
  
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
