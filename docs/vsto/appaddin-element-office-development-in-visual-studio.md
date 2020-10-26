---
title: '&lt;appAddin &gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <appAddin> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1bf9ea990d12bd24adee3f6a24a39fa43c74fb71
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85531639"
---
# <a name="ltappaddingt-element-office-development-in-visual-studio"></a>&lt;appAddin &gt; 要素 (Visual Studio での Office 開発)
  名前空間の **Appaddin** 要素には、 `vstov4` VSTO アドインのカスタマイズ固有の情報が格納されます。

## <a name="syntax"></a>構文

```xml
<appAddin
  application
  loadBehavior
  keyName>
  <friendlyName>
  <description>
  <formRegions></formRegions>
</appAddin>
```

## <a name="elements-and-attributes"></a>要素と属性
 **Appaddin**要素は必須で `vstov4` あり、名前空間にあります。 アプリケーションマニフェストで定義されている **Appaddin** 要素は1つだけです。

 **Appaddin**要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|**application**|必須。 Microsoft Office アプリケーションを指定します。 この値は、Excel、InfoPath、Outlook、PowerPoint、Project、Visio、Word のいずれか 1 つになります。|
|**loadBehavior**|省略可能。 既定では、 **loadBehavior** は、この値をに設定することによって有効になります。 デバッグする場合は、この値を 2 に設定して VSTO アドインを無効にできます。 詳細については、「LoadBehavior Values in the [VSTO アドイン](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。|
|**keyName**|必須。 この値は、アプリケーションが VSTO アドインを読み込むのに使用するレジストリ キーの名前です。 詳細については、「 [VSTO アドインのレジストリエントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。|

 **Appaddin**要素には、次の子要素があります。

### <a name="friendlyname"></a>friendlyName
 省略可能。 **Friendlyname**要素については[&#60;friendlyname&#62; 要素 &#40;Visual Studio での Office 開発&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md)で説明されています。

### <a name="description"></a>description
 省略可能。 **Description**要素については[&#60;description&#62; 要素 &#40;Visual Studio&#41;での Office 開発](../vsto/description-element-office-development-in-visual-studio.md)」を説明しています。

### <a name="formregions"></a>formRegions
 フォーム領域を含んでいる Outlook VSTO アドインでのみ必須です。 **Formregions**要素は[&#60;formregions&#62; 要素 &#40;Visual Studio&#41;での Office 開発](../vsto/formregions-element-office-development-in-visual-studio.md)について説明しています。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、を使用して配置される Outlook ソリューションの **Appaddin** 要素を示してい [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] ます。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
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
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)