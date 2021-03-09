---
title: '&lt;vstoRuntime &gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
description: Vstav3 名前空間の vstoRuntime 要素には、特定の Office ソリューションに対してサポートされているバージョンの Visual Studio Tools for Office ランタイムが含まれています。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <vstoRuntime> element
- <vstoRuntime> element
- vstoRuntime element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7c856836bd2ba107a2fa6c3017c5ecb2694fcf6b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102468573"
---
# <a name="ltvstoruntimegt-element-office-development-in-visual-studio"></a>&lt;vstoRuntime &gt; 要素 (Visual Studio での Office 開発)
  `vstoRuntime` 名前空間の `vstav3` 要素は、特定の Office ソリューション用の、Visual Studio Tools for Office ランタイムのサポートされるバージョンを格納します。

## <a name="syntax"></a>構文

```xml
<vstoRuntime
    release
    version
    supportUrl />
```

## <a name="elements-and-attributes"></a>要素と属性
 `vstoRuntime` 要素は必須です。この要素は `vstav3` 名前空間にあります。 Office ソリューションが 2 つのバージョンの Visual Studio Tools for Office ランタイムをサポートする場合、アプリケーション マニフェストには 2 つの `vstoRuntime` 要素があります。

 `vstoRuntime` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`release`|必須。 Visual Studio Tools for Office ランタイムのリリース バージョン。|
|`version`|必須。 Visual Studio Tools for Office ランタイムのバージョン番号。|
|`supportUrl`|省略可能。 Visual Studio Tools for Office ランタイムのインストール場所へのリンク。|

 `vstoRuntime` には要素がありません。

## <a name="example"></a>例
 次のコード例は、 `vstoRuntime` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

```xml
<vstav3:vstoRuntime
    release="VSTOR40Beta1"
    version="10.0.20303"
    supportUrl="http://www.microsoft.com" />
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
