---
title: '&lt;update &gt; 要素 (Visual Studio での Office 開発)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- update element
- <update> element
- application manifests [Office development in Visual Studio], <update> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5712be9e12ede3338856955e00a34a7565d733ee
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968763"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;update &gt; 要素 (Visual Studio での Office 開発)
  要素は、 `update` ソリューションが更新プログラムをチェックする間隔を指定します。

## <a name="syntax"></a>構文

```xml
<update
  enabled>
  <expiration
    maximumAge
    unit
  />
</update>
```

## <a name="elements-and-attributes"></a>要素と属性
 `update` 要素は必須です。この要素は `vstav3` 名前空間にあります。

 `update` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`enabled`|必須。 Enabled は、次のいずれかの値に設定します。<br /><br /> -   更新プログラムを確認する **場合は true** 。<br />-   更新プログラムがチェックされないようにする場合は **false** 。|

 `update` 要素には、次の子要素があります。

### <a name="expiration"></a>expiration
 `expiration` 要素は必須です。この要素は `vstav3` 名前空間にあります。 この要素は、ソリューションが更新プログラムを確認する間隔を指定します。

 `expiration` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`maximumAge`| 必須。 これを整数と同じ値に設定します。|
|`unit`|必須。 `unit`次のいずれかの値に設定します。<br /><br /> -   **まで**<br />-   **日時**<br />-   **ごと**|

## <a name="example-of-always-checking-for-updates"></a>常に更新プログラムを確認する例

### <a name="description"></a>説明
 次のコード例は、 `update` Office ソリューションで常に更新プログラムをチェックするように設定されている要素を示しています。

### <a name="code"></a>コード

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>既定の更新間隔を設定する例

### <a name="description"></a>説明
 次のコード例は、 `update` Office ソリューションのアプリケーションマニフェストの要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>関連項目

- [ClickOnce を使用して Office ソリューションを配置する](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
