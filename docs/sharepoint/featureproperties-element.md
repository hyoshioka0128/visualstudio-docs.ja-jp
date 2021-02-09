---
title: FeatureProperties 要素 |Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である FeatureProperties 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperties element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8756feaf08de9b01904309177f5e19c122da714d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876720"
---
# <a name="featureproperties-element"></a>FeatureProperties 要素
  SharePoint に配置されるときにフィーチャーに含まれるプロパティ値のコレクション。 フィーチャーが配置されると、コード内のプロパティ値にアクセスできるようになります。

## <a name="syntax"></a>構文

```xml
<FeatureProperties>
  <FeatureProperty.../>
</FeatureProperties>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|省略可能な要素です。<br /><br /> キー/値形式のカスタムプロパティを表します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクトアイテムを表します。 この要素は、ファイルの必須のルート要素です `.spdata` 。|

## <a name="remarks"></a>解説
 機能のプロパティの詳細については、「 [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

## <a name="element-information"></a>要素情報

|要素|説明|
|-------------|-----------------|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
