---
title: '&lt;postActions &gt; 要素 (Office 開発)'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postActions> element
- postActions element
- <postActions> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: da0c3ee640d7ae4ec1b61df7a60893a7e1428cd2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99879437"
---
# <a name="ltpostactionsgt-element-office-development"></a>&lt;postActions &gt; 要素 (Office 開発)
  `postActions` 名前空間の `vstav3` の要素には、Office ソリューションのインストール後に実行する配置後アクションを説明する `postAction` 要素がすべて含まれています。

## <a name="syntax"></a>構文

```xml
<postActions>
  <postAction>
    <entryPoint>
    </entryPoint>
    <postActionData>
    </postActionData>
  </postAction>
</postActions>
```

## <a name="elements-and-attributes"></a>要素と属性
 `postActions` 要素は省略可能であり、 `vstav3` 名前空間にあります。 アプリケーション マニフェストで定義された `postActions` 要素が 1 つだけあります。

 `postActions` 要素に属性はありません。

 `postActions` には、次の要素があります。

### <a name="postaction"></a>postAction
 任意。 `postAction`名前空間の要素のロールは `vstav3` [&#60;postaction&#62; 要素で定義され、Visual Studio&#41;での Office 開発 &#40;](../vsto/postaction-element-office-development-in-visual-studio.md)ます。

## <a name="post-deployment-action-example"></a>配置後アクションの例

### <a name="description"></a>Description
 次のコード例は、 `postActions` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:postActions>
  <vstav3:postAction>
    <vstav3:entryPoint
      class="PostDeploymentAction.PostDeploymentActionSample">
      <assemblyIdentity
        name="PostDeploymentAction"
        version="1.0.0.0"
        language="neutral"
        processorArchitecture="msil" />
    </vstav3:entryPoint>
    <vstav3:postActionData>
    </vstav3:postActionData>
  </vstav3:postAction>
</vstav3:postActions>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
