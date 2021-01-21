---
title: SafeControls 要素 |Microsoft Docs
description: SafeControls 要素に関する情報を取得します。この要素は、SharePoint サイトの ASPX ページでのアクセスのためにセキュリティで保護されているとマークされた ASPX コントロールまたは web パーツのコレクションを保持します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControls element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c3423d1b6efd106ef7f947bd8573dcd1aa548a66
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95440676"
---
# <a name="safecontrols-element"></a>SafeControls 要素
  SharePoint サイトの任意の ASPX ページですべてのユーザーがアクセスできるようにセキュリティで保護されたものとして指定された ASPX コントロールおよび Web パーツのコレクション。

## <a name="syntax"></a>構文

```xml
<SafeControls>
  <SafeControl.../>
</SafeControls>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[SafeControl](../sharepoint/safecontrol-element.md)|省略可能な要素です。<br /><br /> SharePoint サイトの任意の ASPX ページで任意のユーザーがアクセスできるようにセキュリティで保護されていると指定された ASPX コントロールまたは Web パーツを表します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクトアイテムを表します。 この要素は、 *sharepointprojectitem.spdata* ファイルの必須のルート要素です。|

## <a name="remarks"></a>注釈
 安全なコントロールの詳細については、「 [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
