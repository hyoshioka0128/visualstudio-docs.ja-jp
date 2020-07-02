---
title: ProjectItemFolder 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38f8f70cc6480554441809e33c4083735600fbbb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539816"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 要素
  マップされたフォルダーを表します。

## <a name="syntax"></a>構文

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>Type
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**Target**|**Xs: string**属性が必要です。<br /><br /> 配置ルートフォルダーを基準として、マップされたフォルダーが対応する SharePoint インストール内のフォルダーのパスです。 展開ルートフォルダーは、 **type**属性によって指定された展開の種類によって決定されます。<br /><br /> 詳細については、「 [sharepoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の sharepoint プロジェクト項目の**配置パス**と**配置ルート**プロパティの説明を参照してください。|
|**Type**|**Xs: string**属性が必要です。<br /><br /> マップされたフォルダーの配置の種類。 使用可能な値の詳細については、「 [sharepoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の「sharepoint プロジェクト項目の**配置の種類**」プロパティの説明を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクトアイテムを表します。 この要素は、 *sharepointprojectitem.spdata*ファイルの必須のルート要素です。|

## <a name="remarks"></a>Remarks
 マップされたフォルダーの詳細については、「[方法: マップされたフォルダーを追加および削除](../sharepoint/how-to-add-and-remove-mapped-folders.md)する」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**[スキーマ名]**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [方法: マップされたフォルダーを追加および削除する](../sharepoint/how-to-add-and-remove-mapped-folders.md)
