---
title: '&lt;postAction &gt; 要素 (Visual Studio での Office 開発)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postAction> element
- <postAction> element
- postAction element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 149aa0cf8543f5b5b1b5ada18a8b2f0e58f063d0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546940"
---
# <a name="ltpostactiongt-element-office-development-in-visual-studio"></a>&lt;postAction &gt; 要素 (Visual Studio での Office 開発)
  `postAction` 名前空間の `vstav3` 要素には、配置後アクションに関連付ける `entrypoint` 要素とすべての `postActionData` 要素を格納します。これらの要素は、Office ソリューションのインストール後に実行されます。

## <a name="syntax"></a>構文

```xml
<postAction>
  <entryPoint>
  </entryPoint>
  <postActionData>
  </postActionData>
</postAction>
```

## <a name="elements-and-attributes"></a>要素と属性
 `postAction` 要素は省略可能であり、 `vstav3` 名前空間にあります。 アプリケーション マニフェストには、配置後アクションごとに `postAction` 要素を 1 つ定義します。

 `postAction` 要素に属性はありません。

 `postAction` には、次の要素があります。

### <a name="entrypoint"></a>entryPoint
 省略可能。 `entryPoint`名前空間の要素の役割 `vstav3` は、 [Visual Studio&#41;での Office 開発 &#40;&#60;entryPoints&#62; 要素](../vsto/entrypoints-element-office-development-in-visual-studio.md)で定義されています。

### <a name="postactiondata"></a>postActionData
 省略可能。 `postActionData`名前空間の要素のロールは `vstav3` [&#60;postactiondata&#62; 要素で定義され、Visual Studio&#41;での Office 開発 &#40;](../vsto/postactiondata-element-office-development-in-visual-studio.md)ます。

## <a name="post-deployment-action-example"></a>配置後アクションの例

### <a name="description"></a>説明
 次のコード例は、 `postAction` を使用して配置する Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
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
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
