---
title: '&lt;publisherIdentity &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publisherIdentity Element [ClickOnce deployment manifest], introduction
- required element for signed manifests [ClickOnce], publisherIdentity Element
- publisherIdentity Element [ClickOnce deployment manifest], syntax, elements, and attributes
ms.assetid: 34c579db-d2f2-4b66-b9c8-47207f33d950
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 995b002784c1e76ceed36e51edb1ae893448f448
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62927540"
---
# <a name="ltpublisheridentitygt-element-clickonce-deployment"></a>&lt;publisherIdentity &gt; 要素 (ClickOnce 配置)
この配置マニフェストに署名した発行元についての情報が含まれます。

## <a name="syntax"></a>Syntax

```xml
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