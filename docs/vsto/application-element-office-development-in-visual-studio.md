---
title: '&lt;application &gt; 要素 (Visual Studio での Office 開発)'
description: Vstav3 名前空間の application 要素が Office ソリューションの説明をラップする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <application> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 37ab88939b6a5a753f67621697a63903c5a35eb2
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847040"
---
# <a name="ltapplicationgt-element-office-development-in-visual-studio"></a>&lt;application &gt; 要素 (Visual Studio での Office 開発)
  `application` 名前空間の `vstav3` 要素は、Office ソリューションの説明をラップします。 ドキュメント レベルのカスタマイズと VSTO アドインでは、子要素が異なります。

## <a name="syntax-for-document-level-customizations"></a>ドキュメントレベルのカスタマイズの構文

```xml
<application>
  <customization
    id
    <document
      solutionId
    />
  </customization>
</application>
```

## <a name="syntax-for-application-level-add-ins"></a>アプリケーションレベルのアドインの構文

```xml
<application>
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
</application>
```

## <a name="elements-and-attributes"></a>要素と属性
 `application` 名前空間の `vstav3` 要素は、 `vstov4` 名前空間に格納されている、カスタマイズに固有のすべての情報をラップするノードです。

 `application` 要素に属性はありません。

 `application` 要素には次の要素があります。

### <a name="customization"></a>カスタマイズ
 `customization`名前空間の要素のロールは `vstov3` [&#60;カスタマイズ&#62; 要素 &#40;Visual Studio&#41;での Office 開発](../vsto/customization-element-office-development-in-visual-studio.md)に定義されています。

## <a name="document-level-customization-example"></a>ドキュメントレベルのカスタマイズの例

### <a name="description"></a>説明
 次のコード例は `application` を使用して配置されるドキュメント レベルの Office ソリューションの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「 [Application Manifests for Office Solutions](../vsto/application-manifests-for-office-solutions.md)」に記載されている例の一部を抜粋したものです。

### <a name="code"></a>コード

```xml
<vstav3:application>
  <vstov4:customizations
    xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
    <vstov4:customization>
      <vstov4:document
        solutionId="73e" />
    </vstov4:customization>
  </vstov4:customizations>
</vstav3:application>
```

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は `application` を使用して配置されるアプリケーション レベルの Office ソリューションの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、「 [Application Manifests for Office Solutions](../vsto/application-manifests-for-office-solutions.md)」に記載されている例の一部を抜粋したものです。

### <a name="code"></a>コード

```xml
<vstav3:application>
  <vstov4:customizations
    xmlns:vstov4="urn:schemas-microsoft-com:vsto.v4">
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
  </vstov4:customizations>
</vstav3:application>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)