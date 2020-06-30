---
title: ProjectOutputFile 要素 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectOutputFile element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 12f399b7a09c18c77482475575ca387a11955762
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542390"
---
# <a name="projectoutputfile-element"></a>ProjectOutputFile 要素
  SharePoint に配置されるときにプロジェクト項目に含める、個別のプロジェクトの出力を表します。

## <a name="syntax"></a>構文

```xml
<ProjectOutputFile ProjectId = "GUID of the project"
    ProjectPath = "Relative path of the project"
    Target = "Deployment path of the project output"
    Type = "Type of deployment for the project output" />
```

## <a name="type"></a>Type
 **ProjectOutputFileType**

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|**ProjectId**|**Xs: string**属性が必要です。<br /><br /> 出力が含まれている依存プロジェクトの GUID。 これは、依存プロジェクトファイルの**Projectguid**要素に対応します。|
|**ProjectPath**|**Xs: string**属性が必要です。<br /><br /> プロジェクトファイル名を含む、出力が含まれる依存プロジェクトの相対パスを指定します。 このパスは、SharePoint プロジェクトアイテムを含む SharePoint プロジェクトのルートフォルダーに対する相対パスです。|
|**Target**|**Xs: string**属性 (省略可能)。<br /><br /> 配置ルートフォルダーを基準として、SharePoint サーバーに依存プロジェクトの出力を配置するパス。 展開ルートフォルダーは、 **type**属性によって指定された展開の種類によって決定されます。<br /><br /> 詳細については、「 [sharepoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の sharepoint プロジェクト項目の**配置パス**と**配置ルート**プロパティの説明を参照してください。|
|**Type**|**Xs: string**属性が必要です。<br /><br /> 依存プロジェクトの出力に使用する配置の種類。 使用可能な値の詳細については、「 [sharepoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)」の「sharepoint プロジェクト項目の**配置の種類**」プロパティの説明を参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[[ファイル]](../sharepoint/files-element.md)|Sharepoint に配置されるときに SharePoint プロジェクト項目に含めるファイルを指定します。|

## <a name="remarks"></a>Remarks
 **ProjectOutputFile**要素を使用して、SharePoint プロジェクトアイテムの配置にプロジェクトの出力を含めます。 別のプロジェクト、またはプロジェクトアイテムを含む同じプロジェクトを指定できます。 詳細については、「[プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)」を参照してください。

## <a name="element-information"></a>要素情報

|プロパティ|値|
|-|-|
|**Namespace**|http: \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**[スキーマ名]**|SharePoint プロジェクトアイテムスキーマ|
|**検証ファイル**|ProjectItemModelSchema|
|**空にすることができます**|いいえ|

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)
- [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
