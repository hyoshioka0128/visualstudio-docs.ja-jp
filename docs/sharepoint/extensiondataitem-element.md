---
title: ExtensionDataItem 要素 |Microsoft Docs
description: ExtensionDataItem 要素に関する参照情報を表示します。これは、SharePoint プロジェクト項目スキーマの要素です。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionDataItem element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 23bd231343b3e7a6c68883aa7fe3ee4e518ac883
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672614"
---
# <a name="extensiondataitem-element"></a>ExtensionDataItem 要素
  SharePoint プロジェクト項目に関連付けられているカスタムデータ項目 (キー/値の形式)。 キーと値は、どちらも文字列である必要があります。

## <a name="syntax"></a>構文

```xml
<ExtensionDataItem Key = "Key of the data item"
    Value = "Value of the data item" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**[キー]**|**Xs: string** 属性が必要です。<br /><br /> データ項目を格納および取得するために使用されるキー。|
|**Value**|**Xs: string** 属性が必要です。<br /><br /> データ項目の値。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|SharePoint プロジェクトアイテムに関連付けられているカスタムデータアイテムのコレクションを表します。|

## <a name="remarks"></a>注釈
 オブジェクトのプロパティを使用してカスタムデータを SharePoint プロジェクトアイテムに関連付けると <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 、Visual Studio は、そのデータをプロジェクトアイテムのファイルの新しい **extensiondataitem** 要素に保存し `.spdata` ます。 詳細については、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**スキーマ名**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
