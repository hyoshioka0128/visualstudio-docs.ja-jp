---
title: '&lt;postActionData &gt; 要素 (Visual Studio での Office 開発)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <postActionData> element
- application manifests [Office development in Visual Studio], <postActionData> element
- postActionData element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 104af55fdc11b6afae757eff95a964dad83418a6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85541870"
---
# <a name="ltpostactiondatagt-element-office-development-in-visual-studio"></a>&lt;postActionData &gt; 要素 (Visual Studio での Office 開発)
  `postActionData` 名前空間の `vstav3` 要素は、Office ソリューションをインストールした後に実行されるすべての配置後アクションに関連付けられているデータを指定します。

## <a name="syntax"></a>構文

```xml
<postActionData>
</postActionData>
```

## <a name="elements-and-attributes"></a>要素と属性
 `postActionData` 要素は省略可能であり、 `vstav3` 名前空間にあります。 アプリケーション マニフェストには、配置後アクションごとに `postActionData` 要素を 1 つ定義します。

 `postActions` 要素に属性はありません。

 `postActions` に子要素はありません。

## <a name="post-deployment-action-example"></a>配置後アクションの例

### <a name="description"></a>説明
 次のコード例は、 `postAction` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:postActionData>
  data in any format
</vstav3:postActionData>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
