---
title: '&lt;assembly &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
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
- <assembly> element [ClickOnce application manifest]
ms.assetid: 51410569-10f9-4c0a-96b5-d39185edbefc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d619b8b3cd81e5b00fc689077a95ade08f4d7eed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183479"
---
# <a name="ltassemblygt-element-clickonce-application"></a>&lt;assembly &gt; 要素 (ClickOnce アプリケーション)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションマニフェストの最上位要素。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      <assembly  
   manifestVersion  
/>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 `assembly`要素はルート要素であり、必須です。 最初に含まれる要素は、要素である必要があり `assemblyIdentity` ます。 マニフェスト要素は、次のいずれかの名前空間にある必要があります。  
  
 `urn:schemas-microsoft-com:asm.v1`  
  
 `urn:schemas-microsoft-com:asm.v2`  
  
 `http://www.w3.org/2000/09/xmldsig#`  
  
 アセンブリの子要素は、継承またはタグ付けによって、これらの名前空間にも存在する必要があります。  
  
 `assembly` 要素には、次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`manifestVersion`|必須です。 `manifestVersion`属性をに設定する必要があり `1.0` ます。|  
  
## <a name="example"></a>例  
 次のコード例は、アプリケーションマニフェストの要素を示してい `assembly` [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 このコード例は、 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)に用意されている大規模な例の一部です。  
  
```  
<asmv1:assembly   
  xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"   
  manifestVersion="1.0"   
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)   
 [\<assembly> 要素](../deployment/assembly-element-clickonce-deployment.md)
