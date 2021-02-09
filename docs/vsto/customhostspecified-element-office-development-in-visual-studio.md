---
title: '&lt;customHostSpecified の &gt; 要素 (Visual Studio での Office 開発)'
description: CustomHostSpecified の要素が、このソリューションがスタンドアロンアプリケーションではないことを示す方法を説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customHostSpecified> element
- <customHostSpecified> element
- customHostSpecified element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ba5ce54e862862c1e6750c78416fec4d5cf51cdd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99849984"
---
# <a name="ltcustomhostspecifiedgt-element-office-development-in-visual-studio"></a>&lt;customHostSpecified の &gt; 要素 (Visual Studio での Office 開発)
  要素は、 `customHostSpecified` このソリューションがスタンドアロンアプリケーションではないことを示します。 Office ソリューションには Microsoft Office アプリケーション内でホストされるコンポーネントが含まれています。

## <a name="syntax"></a>構文

```xml
<customHostSpecified />
```

## <a name="elements-and-attributes"></a>要素と属性
 `customHostSpecified`Office ソリューションには要素が必要です。 この要素は名前空間に含まれ `co.v1` ており、この配置には、カスタムホストの内部に配置され、スタンドアロンアプリケーションではないコンポーネントが含まれていることを指定します。

 この要素は、アプリケーションマニフェスト内の最初の要素の子です `<entrypoint>` 。 その要素に他の子要素を指定することはできません `<entrypoint>` 。また、 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] インストール中に検証エラーが発生します。

 この要素には属性がなく、子要素もありません。

## <a name="example"></a>例
 次のコード例は、 `customHostSpecified` Office ソリューションのアプリケーションマニフェストの要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)