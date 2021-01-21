---
title: FeatureProperty 要素 |Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である FeatureProperty 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8e6010ac45d0b760325c73c4bd754fbb0b422a77
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672757"
---
# <a name="featureproperty-element"></a>FeatureProperty 要素
  SharePoint に配置されるときにフィーチャーに含まれるカスタムプロパティを表します。 フィーチャーが配置された後、コード内のプロパティにアクセスできます。

## <a name="syntax"></a>構文

```xml
<FeatureProperty Key = "Key of the property value"
    Value = "Property value" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**[キー]**|**Xs: string** 属性が必要です。<br /><br /> プロパティ値を格納および取得するために使用されるキー。 各プロパティには、機能内で一意のキーが必要です。|
|**Value**|**Xs: string** 属性が必要です。<br /><br /> プロパティ値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|SharePoint に配置されるときにフィーチャーに含まれるプロパティ値のコレクションを表します。|

## <a name="remarks"></a>注釈
 機能のプロパティの詳細については、「 [プロジェクト項目でのパッケージと配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

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
