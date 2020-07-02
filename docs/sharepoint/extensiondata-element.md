---
title: ExtensionData 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionData element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3b700239f97153cef94ab1d7010ad16ed9aa6001
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546563"
---
# <a name="extensiondata-element"></a>ExtensionData 要素
  SharePoint プロジェクトアイテムに関連付けられているカスタムデータアイテムのコレクションを表します。

## <a name="syntax"></a>構文

```xml
<ExtensionData>
  <ExtensionDataItem.../>
</ExtensionData>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|省略可能な要素です。<br /><br /> SharePoint プロジェクト項目に関連付けられているカスタムデータ項目を表します (キー/値の形式)。 キーと値は、どちらも文字列である必要があります。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|SharePoint プロジェクトアイテムを表します。 この要素は、ファイルの必須のルート要素です `.spdata` 。|

## <a name="remarks"></a>Remarks
 オブジェクトのプロパティを使用してカスタムデータを SharePoint プロジェクトアイテムに関連付けると、Visual Studio によって、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> プロジェクトアイテムのファイルの**extensiondata**要素にデータが保存され `.spdata` ます。 詳細については、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**[スキーマ名]**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
