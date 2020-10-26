---
title: '&lt;publisherIdentity &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 486e0bc5059e041f02e8dac4836c5ff59b27f63e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157632"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity &gt; 要素 (ClickOnce 配置)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この配置マニフェストに署名した発行元についての情報が含まれます。  
  
## <a name="syntax"></a>Syntax  
  
```  
<publisherIdentity  
   name  
   issuerKeyHash  
/>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 `publisherIdentity`署名されたマニフェストには要素が必要です。 次の表は、要素がサポートする属性を示して `publisherIdentity` います。  
  
|属性|説明|  
|---------------|-----------------|  
|`name`|必須です。 このアプリケーションを発行したパーティの id を記述します。|  
|`issuerKeyHash`|必須です。 証明書の発行者の公開キーの SHA-1 ハッシュを格納します。|  
  
#### <a name="parameters"></a>パラメーター  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
  
## <a name="subhead"></a>小見出し
