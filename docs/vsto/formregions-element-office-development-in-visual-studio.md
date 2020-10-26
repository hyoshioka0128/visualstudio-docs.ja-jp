---
title: '&lt;formRegions &gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formRegions element
- <formRegions> element
- application manifests [Office development in Visual Studio], <formRegions> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6f98c74c2df998f0e79f5b95a316a7917304e029
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538360"
---
# <a name="ltformregionsgt-element-office-development-in-visual-studio"></a>&lt;formRegions &gt; 要素 (Visual Studio での Office 開発)
  `formRegions`名前空間の要素には `vstov4` 、VSTO アドインに関連付けられている Microsoft Office Outlook フォーム領域が含まれます。

## <a name="syntax"></a>構文

```xml
<formRegions>
  <formRegion>
  </formRegion>
</formRegions>
```

## <a name="elements-and-attributes"></a>要素と属性
 `formRegions` 名前空間の `vstov4` 要素には、Outlook VSTO アドインの `formRegion` 要素がすべて含まれています。 それは、フォーム領域のある Outlook VSTO アドインにのみ必要です。

 アプリケーション マニフェストで定義できる `formRegions` 要素は 1 つだけです。

 `formRegions` 要素に属性はありません。

 `formRegions` 要素には次の要素があります。

### <a name="formregion"></a>formRegion
 フォーム領域のある Outlook VSTO アドインに必要です。 `formRegion`要素は&#60;formRegion&#62; 要素で定義され、 [Visual Studio&#41;での Office 開発 &#40;](../vsto/formregion-element-office-development-in-visual-studio.md)ます。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、 `formRegions` を使用して展開したアプリケーション レベルの Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:formRegions>
  <vstov4:formRegion
      name="OutlookAddIn1.FormRegion1">
    <vstov4:messageClass name="IPM.Note" />
    <vstov4:messageClass name="IPM.Contact" />
    <vstov4:messageClass name="IPM.Appointment" />
  </vstov4:formRegion>
</vstov4:formRegions>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)