---
title: '&lt;description &gt; 要素 (Visual Studio での Office 開発)'
description: Vstov4 名前空間の description 要素に、[COM アドイン] ダイアログボックスに表示される Office ソリューションの説明が格納されていることを確認してください。
titleSuffix: ''
ms.custom: secdec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- description element
- <description> element
- application manifests [Office development in Visual Studio], <description> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9f065dd07e901ee0d59b39f1096cc351cd70bc02
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897600"
---
# <a name="ltdescriptiongt-element-office-development-in-visual-studio"></a>&lt;description &gt; 要素 (Visual Studio での Office 開発)
  `description` 名前空間の `vstov4` 要素は、Microsoft Office アプリケーションの [COM アドイン] ダイアログ ボックスに表示される Office ソリューションの説明を格納します。

## <a name="syntax"></a>構文

```xml
<description>
</description>
```

## <a name="elements-and-attributes"></a>要素と属性
 任意。 `description` 要素は `vstov4` 名前空間に属します。 この要素は、Microsoft Office アプリケーションの [COM アドイン] ダイアログ ボックスに表示されるアドインの説明を格納します。

 `description` 要素には、属性も要素もありません。

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>Description
 次のコード例は、 `description` を使用して配置されるアプリケーションレベルのソリューションの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstov4:description>
  ContosoOutlookAddIn - Outlook add-in
  created with Visual Studio Tools for Office
</vstov4:description>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)