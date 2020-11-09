---
title: '&lt;fileAssociation &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
description: FileAssociation 要素は、アプリケーションに関連付けられるファイル拡張子を識別します。 FileAssociation 要素は省略可能です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <fileAssociation> element [ClickOnce application manifest]
- manifests [ClickOnce], fileAssociation element
ms.assetid: 8f951b4f-54f9-412e-a9e5-af4e379fcf08
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f1908b4f63edcf90643c28523c0c6ed0d0e11a97
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382729"
---
# <a name="ltfileassociationgt-element-clickonce-application"></a>&lt;fileAssociation &gt; 要素 (ClickOnce アプリケーション)
アプリケーションに関連付けるファイル拡張子を識別します。

## <a name="syntax"></a>構文

```xml
<fileAssociation
    xmlns="urn:schemas-microsoft-com:clickonce.v1"
    extension
    description
    progid
    defaultIcon
/>
```

## <a name="elements-and-attributes"></a>要素と属性
 `fileAssociation` 要素は省略可能です。 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`extension`|必須。 アプリケーションに関連付けられるファイル拡張子。|
|`description`|必須。 シェルによって使用されるファイルの種類の説明。|
|`progid`|必須。 ファイルの種類を一意に識別する名前。|
|`defaultIcon`|必須。 この拡張子を持つファイルに使用するアイコンを指定します。 アイコンファイルは、この要素を含む[ \<assembly> 要素](../deployment/assembly-element-clickonce-application.md)内の[ \<file> 要素](../deployment/file-element-clickonce-application.md)を使用して指定する必要があります。|

## <a name="remarks"></a>Remarks
 この要素には、"urn: schema-microsoft-com: clickonce. v1" への XML 名前空間参照が含まれている必要があります。 要素を使用する場合は `<fileAssociation>` 、親要素の要素の後に指定する必要があり `<application>` [ \<assembly> ](../deployment/assembly-element-clickonce-application.md)ます。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 既存のファイルの関連付けは上書きされません。 ただし、ClickOnce アプリケーションでは、現在のユーザーのみのファイル拡張子をオーバーライドできます。 ClickOnce アプリケーションがアンインストールされると、ClickOnce によってユーザーのファイルの関連付けが削除され、コンピューターごとの関連付けが再びアクティブになります。

## <a name="example"></a>例
 次のコード例は、 `fileAssociation` を使用して配置されたテキストエディターアプリケーションのアプリケーションマニフェストの要素を示してい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 このコード例には、属性に必要な[ \<file> 要素](../deployment/file-element-clickonce-application.md)も含まれてい `defaultIcon` ます。

```xml
<file name="text.ico" size="4286">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>0joAqhmfeBb93ZneZv/oTMP2brY=</dsig:DigestValue>
  </hash>
</file>
<file name="writing.ico" size="9662">
  <hash>
    <dsig:Transforms>
      <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
    </dsig:Transforms>
    <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
    <dsig:DigestValue>2cL2U7cm13nG40v9MQdxYKazIwI=</dsig:DigestValue>
  </hash>
</file>
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".text" description="Text  Document (ClickOnce)" progid="Text.Document" defaultIcon="text.ico" />
<fileAssociation xmlns="urn:schemas-microsoft-com:clickonce.v1" extension=".writing" description="Writings (ClickOnce)" progid="Writing.Document" defaultIcon="writing.ico" />
```

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)