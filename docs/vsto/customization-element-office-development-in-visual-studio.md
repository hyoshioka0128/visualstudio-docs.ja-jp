---
title: '&lt;customization &gt; 要素 (Visual Studio での Office 開発)'
description: Vstov4 名前空間のカスタマイズ要素が特定の Office ソリューションについて記述する方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customization> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e63b93728f41dcff360da8ee9d14e2830d216be5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99849945"
---
# <a name="ltcustomizationgt-element-office-development-in-visual-studio"></a>&lt;customization &gt; 要素 (Visual Studio での Office 開発)
  `customization` 名前空間の `vstov4` 要素では、特定の Office ソリューションについて記述します。 ドキュメント レベルのカスタマイズと VSTO アドインでは、子要素が異なります。

## <a name="syntax-for-document-level-customizations"></a>ドキュメントレベルのカスタマイズの構文

```xml
<customization
  id
  <document
    solutionId
  />
</customization>
```

## <a name="syntax-for-vsto-add-ins"></a>VSTO アドインの構文

```xml
<customization
  id
  <appAddin
    application
    loadBehavior
    keyName>
  <friendlyName></friendlyName>
  <description></description>
  <formRegions></formRegions>
</customization>
```

## <a name="elements-and-attributes"></a>要素と属性
 `customization` 要素には、カスタマイズ固有の情報が含まれています。 この要素は、名前空間 `vstov4=urn:schemas-microsoft-com:vsto.v4`に存在する必要があります。 Office ソリューションごとに、 `customization` 要素が 1 つあります。 たとえば、複数プロジェクトの配置で 3 つの Office ソリューションを配置する場合は、アプリケーション マニフェストに 3 つの `customization` 要素を定義します。

 アセンブリの子要素もこの名前空間に属している必要があります。

 `customization` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`id`|複数プロジェクトの配置の場合は必須です。 `id` 要素によって、Office ソリューションを一意に識別します。|

### <a name="document-level-customizations"></a>カスタマイズの Document-Level
 `customization` 要素には、次の子要素があります。

#### <a name="document"></a>ドキュメント
 `document`名前空間の要素 `vstov4` は[&#60;document&#62; 要素 &#40;Visual Studio&#41;での Office 開発](../vsto/document-element-office-development-in-visual-studio.md)に定義されています。

### <a name="vsto-add-ins"></a>VSTO アドイン
 `customization` 要素には、次の子要素があります。

#### <a name="appaddin"></a>appAddin
 `appAddin`名前空間の要素 `vstov4` は[&#60;appaddin&#62; 要素で定義され、Visual Studio&#41;での Office 開発 &#40;](../vsto/appaddin-element-office-development-in-visual-studio.md)ます。

## <a name="example-of-a-document-level-customization"></a>ドキュメントレベルのカスタマイズの例

### <a name="description"></a>Description
 次のコード例は、ドキュメント レベルのカスタマイズの `customization` 要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:customization>
  <vstov4:document
    solutionId="73e" />
</vstov4:customization>
```

## <a name="example-of-a-vsto-add-in"></a>VSTO アドインの例

### <a name="description"></a>Description
 次のコード例は、 `customization` VSTO アドインの要素を示しています。 この例は、フォーム領域が含まれた Outlook VSTO アドインです。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:customization>
  <vstov4:appAddIn
    application="Outlook"
    loadBehavior="3"
    keyName="ContosoOutlookAddIn">
    <vstov4:friendlyName>
      ContosoOutlookAddIn
    </vstov4:friendlyName>
    <vstov4:description>
      ContosoOutlookAddIn - Outlook VSTO Add-in
      created with Visual Studio Tools for Office
    </vstov4:description>
    <vstov4:formRegions>
      <vstov4:formRegion
          name="OutlookAddIn1.FormRegion1">
        <vstov4:messageClass name="IPM.Note" />
        <vstov4:messageClass name="IPM.Contact" />
        <vstov4:messageClass name="IPM.Appointment" />
      </vstov4:formRegion>
    </vstov4:formRegions>
  </vstov4:appAddIn>
</vstov4:customization>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)