---
title: '&lt;assemblyIdentity &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assemblyIdentity> element [ClickOnce deployment manifest]
ms.assetid: f4a3bb83-c800-47d0-9905-9a5ae2486838
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bfc2ff97a2eb465fe7306ebe368a20e2a7fd8638
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155723"
---
# <a name="ltassemblyidentitygt-element-clickonce-deployment"></a>&lt;assemblyIdentity &gt; 要素 (ClickOnce 配置)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションのプライマリアセンブリを識別し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      <assemblyIdentity    
   name   
   version  
   publicKeyToken  
   processorArchitecture  
    type  
/>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 `assemblyIdentity` 要素は必須です。 子要素は含まれず、次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`name`|必須です。 情報提供を目的として、ユーザーが判読できる配置名を識別します。<br /><br /> に `name` 1 つまたは二重引用符などの特殊文字が含まれている場合、アプリケーションのアクティブ化に失敗する可能性があります。|  
|`version`|必須です。 次の形式でアセンブリのバージョン番号を指定します `major.minor.build.revision` 。<br /><br /> アプリケーションの更新をトリガーするには、この値を更新されたマニフェストでインクリメントする必要があります。|  
|`publicKeyToken`|必須です。 配置マニフェストの署名に使用される公開キーの SHA-1 ハッシュ値の最後の8バイトを表す16文字の16進数文字列を指定します。 署名に使用する公開キーは、2048ビット以上である必要があります。<br /><br /> アセンブリに署名することをお勧めしますが、省略可能ですが、この属性は必須です。 アセンブリが署名されていない場合は、自己署名アセンブリから値をコピーするか、すべてゼロの "ダミー" 値を使用する必要があります。|  
|`processorArchitecture`|必須です。 プロセッサを指定します。 有効な値は、 `msil` 32 ビット windows の場合はすべてのプロセッサ、64ビット windows の場合は、 `x86` `IA64` `Itanium` Intel 64 ビット Itanium プロセッサの場合はです。|  
|`type`|必須です。 Windows サイドバイサイドインストールテクノロジとの互換性を確保します。 使用できる値はのみ `win32` です。|  
  
## <a name="remarks"></a>注釈  
  
## <a name="example"></a>例  
 次のコード例は、 `assemblyIdentity` 配置マニフェストの要素を示してい [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 このコード例は、「 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md) 」で提供されている、より大きな例の一部です。  
  
```  
<!-- Identify the deployment. -->  
<assemblyIdentity   
  name="My Application Deployment.app"  
  version="1.0.0.0"  
  publicKeyToken="43cb1e8e7a352766"  
  language="neutral"  
  processorArchitecture="x86"  
  xmlns="urn:schemas-microsoft-com:asm.v1" />  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)   
 [\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)
