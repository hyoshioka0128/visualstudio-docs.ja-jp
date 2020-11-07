---
title: '&lt;Signature &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
description: Signature 要素には、この配置マニフェストにデジタル署名するために必要な情報が含まれています。 配置マニフェストへの署名は省略できますが、推奨されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <Signature> element [ClickOnce deployment manifest]
ms.assetid: c99b07ad-e8ba-43f2-b0d6-3745e7a7c8b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b7a86236087bdbff8cf82ca4821573f9f799d019
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349283"
---
# <a name="ltsignaturegt-element-clickonce-deployment"></a>&lt;Signature &gt; 要素 (ClickOnce 配置)
この配置マニフェストにデジタル署名するために必要な情報が含まれます。

## <a name="syntax"></a>構文

```xml

<Signature> 
   XML signature information 
</Signature>
```

## <a name="remarks"></a>解説
 エンベロープ署名を使用した配置マニフェストへの署名はオプションですが、推奨されます。 XML ファイルに署名する方法の詳細については、「」で説明されている World Wide Web コンソーシアムの推奨事項「XML 署名の構文と処理」を参照してください [http://www.w3.org/TR/xmldsig-core/](https://www.w3.org/TR/xmldsig-core/) 。

 マニフェストに署名する場合は、すべてのファイルに対してハッシュを指定する必要があります。 ハッシュされていないファイルを含むマニフェストに署名することはできません。これは、ハッシュされていないファイルの内容をユーザーが確認できないためです。

## <a name="example"></a>例
 次のコード例は、 `Signature` 配置で使用される配置マニフェストの要素を示してい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

```xml
<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
  <SignedInfo>
    <CanonicalizationMethod Algorithm=
           "http://www.w3.org/TR/2001/REC-xml-c14n-20010315" />
    <SignatureMethod Algorithm=
           "http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
    <Reference URI="">
      <Transforms>
        <Transform Algorithm=
           "http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
      </Transforms>
      <DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
      <DigestValue>d2z5AE...</DigestValue>
    </Reference>
  </SignedInfo>
  <SignatureValue>
4PHj6SaopoLp...
  </SignatureValue>
  <KeyInfo>
    <X509Data>
      <X509Certificate>
MIIHnTCCBoWgAwIBAgIKJY9+nwAHAAB...
      </X509Certificate>
    </X509Data>
  </KeyInfo>
</Signature>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
