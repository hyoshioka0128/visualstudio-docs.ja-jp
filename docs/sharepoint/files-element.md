---
title: Files 要素 |Microsoft Docs
description: SharePoint プロジェクト項目スキーマの要素である Files 要素に関する参照情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Files element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 03473f40bb78c866f3d93dea11a20b8747afad7b
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672809"
---
# <a name="files-element"></a>Files 要素
  SharePoint プロジェクトアイテムと共に配置するファイルを指定します。たとえば、フィーチャー要素ファイルや SharePoint 以外の依存プロジェクトの出力などです。

## <a name="syntax"></a>構文

```xml
<Files>
  <ProjectItemFile.../>
  <ProjectOutputFile.../>
</Files>
```

## <a name="type"></a>Type
 **FileCollectionType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|省略可能な **ProjectItemFileType** 要素。<br /><br /> SharePoint に配置されるときにプロジェクト項目に含める、フィーチャー要素ファイルなどの SharePoint ファイルを表します。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|省略可能な **Projectoutputfiletype** 要素です。<br /><br /> SharePoint に配置されるときにプロジェクト項目に含めるプロジェクトの出力を表します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクトアイテムを表します。 この要素は、ファイルの必須のルート要素です `.spdata` 。|

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
