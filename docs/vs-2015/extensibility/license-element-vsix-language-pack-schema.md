---
title: License 要素 (VSIX 言語パックスキーマ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
ms.assetid: 57dac3b7-0cdd-405c-9af5-30ed9ca45e53
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f1299d97cbda78049732d3367a9231272397e2ec
ms.sourcegitcommit: 26178b116cbf7353fee6ca989b8d872114f7b405
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284383"
---
# <a name="license-element-vsix-language-pack-schema"></a>要素 (VSIX 言語パックのスキーマ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

省略可能。 拡張機能のライセンスファイルのローカライズ版のパス。  
  
## <a name="syntax"></a>構文  
  
```  
<License>FilePath\license.txt</License>  
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
 表示するローカライズされたライセンスファイルの相対パス。  
  
## <a name="remarks"></a>解説  
 要素が定義されている場合は、指定された `License` ライセンスファイルのテキストがセットアップ中に表示され、ユーザーはライセンスに同意しないと続行できません。  
  
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
