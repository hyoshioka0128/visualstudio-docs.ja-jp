---
title: '&lt;assembly &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#assembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <assembly> element [ClickOnce deployment manifest]
ms.assetid: b8e3362a-f821-4696-b98d-571d4bbfe431
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3b77cfacf3dca2c2cc20d674f79929e9958a16d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155736"
---
# <a name="ltassemblygt-element-clickonce-deployment"></a>&lt;assembly &gt; 要素 (ClickOnce 配置)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

配置マニフェストの最上位要素。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      <assembly    
   manifestVersion  
/>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 `assembly`要素はルート要素であり、必須です。 最初に含まれる要素は、要素である必要があり `assemblyIdentity` ます。 マニフェスト要素は、、、およびの各名前空間にある必要があり `urn:schemas-microsoft-com:asm.v1` `urn:schemas-microsoft-com:asm.v2` `http://www.w3.org/2000/09/xmldsig#` ます。 アセンブリの子要素は、継承またはタグ付けによって、これらの名前空間にも存在する必要があります。  
  
 `assembly` 要素には、次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`manifestVersion`|必須です。 この属性は、に設定する必要があり `1.0` ます。|  
  
## <a name="example"></a>例  
 次のコード例は、 `assembly` を使用して配置されたアプリケーションの配置マニフェストの要素を示してい [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 このコード例は、「 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md) 」で提供されている、より大きな例の一部です。  
  
```  
<asmv1:assembly   
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"  
  manifestVersion="1.0"  
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)   
 [\<assembly> 要素](../deployment/assembly-element-clickonce-application.md)
