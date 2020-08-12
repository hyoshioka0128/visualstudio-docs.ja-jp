---
title: VSIXLanguagePack 要素 (VSIX 言語パックスキーマ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 767f5c22-8b87-49ca-92aa-a7a3f026469f
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cd3ed1477d1c4d345e5fc6f6496d12044d4af244
ms.sourcegitcommit: d9254e54079ae01cdf2d07b11f988faf688f80fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88114233"
---
# <a name="vsixlanguagepack-element-vsix-language-pack-schema"></a>VSIXLanguagePack 要素 (VSIX 言語パックのスキーマ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必須。 VSIX 言語パックのルート要素を提供します。 VSIX 言語パックは、VSIX パッケージのローカライズされたインストール情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```  
<VSIXLanguagePack>  
  <LocalizedName>...</LocalizedName>  
  <LocalizedDescription>...</LocalizedDescription>  
  <MoreInfoURL>...</MoreInfoURL>  
  <License>...</License>  
</VSIXLanguagePack>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`xmlns`|VSIX 言語パックスキーマが定義されている XML 名前空間。|  
  
## <a name="xmlns-attribute"></a>xmlns 属性  
  
|[値]|説明|  
|-----------|-----------------|  
|`http://schemas.microsoft.com/developer/vsx-schema-lp/2010`|必須。 言語パックのスキーマを定義するファイルの場所です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[LocalizedName 要素](../extensibility/localizedname-element-vsix-language-pack-schema.md)|必須。 インストールする拡張機能のローカライズされた名前。|  
|[LocalizedDescription 要素](../extensibility/localizeddescription-element-vsix-language-pack-schema.md)|必須。 インストールする拡張機能のローカライズされた説明。|  
|[MoreInfoURL 要素](../extensibility/moreinfourl-element-vsix-language-pack-schema.md)|省略可能。 拡張機能に関するローカライズされた情報へのリンク。|  
|[License 要素](../extensibility/license-element-vsix-language-pack-schema.md)|省略可能。 拡張機能のライセンスファイルのローカライズ版のパス。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|なし||  
  
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
        いいえ
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>参照  
 [VSX Language Pack スキーマリファレンス](../extensibility/vsx-language-pack-schema-reference.md) [vsix パッケージのローカライズ](../extensibility/localizing-vsix-packages.md) [vsix 拡張スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
