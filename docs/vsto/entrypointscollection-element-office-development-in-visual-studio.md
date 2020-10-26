---
title: '&lt;entryPointsCollection &gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <entryPointsCollection> element
- application manifests [Office development in Visual Studio], <entryPointsCollection> element
- entryPointsCollection element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ffa3c76f0f1afa0c9c445cfaf6f5f92484a73ba7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543560"
---
# <a name="ltentrypointscollectiongt-element-office-development-in-visual-studio"></a>&lt;entryPointsCollection &gt; 要素 (Visual Studio での Office 開発)
  `entryPointsCollection` 名前空間の `vstav3` 要素は、Office ソリューションに関連付けられているすべての `entryPoints` 要素を格納します。

## <a name="syntax"></a>構文

```xml
<entryPointsCollection>
  <entryPoints>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
    <entryPoint>
    </entryPoint>
  </entryPoints>
</entryPointsCollection>
```

## <a name="elements-and-attributes"></a>要素と属性
 `entryPointsCollection` 要素は必須です。この要素は `vstav3` 名前空間にあります。 子要素もこの名前空間に属している必要があります。 アプリケーション マニフェストで定義された `entryPointsCollection` 要素が 1 つだけあります。

 `entryPointsCollection` 要素に属性はありません。

 `entryPointsCollection` には、次の要素があります。

### <a name="entrypoints"></a>entryPoints
 必須。 `entryPoints`名前空間の要素の役割 `vstav3` は、 [Visual Studio&#41;での Office 開発 &#40;&#60;entryPoints&#62; 要素](../vsto/entrypoints-element-office-development-in-visual-studio.md)で定義されています。

## <a name="document-level-customization-example"></a>ドキュメントレベルのカスタマイズの例

### <a name="description"></a>説明
 次のコード例では、 `entryPointsCollection` を使用して配置したドキュメント レベルのソリューションのアプリケーション マニフェストにある [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.ThisWorkbook">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet1">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet2">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
      <vstav3:entryPoint
        class="ContosoExcelWorkbook.Sheet3">
        <assemblyIdentity
          name="ContosoExcelWorkbook"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
```

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例では、 `entryPointsCollection` を使用して配置したアプリケーション レベルのソリューションのアプリケーション マニフェストにある [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:entryPointsCollection>
    <vstav3:entryPoints>
      <vstav3:entryPoint
        class="ContosoOutlookAddIn.ThisAddIn">
        <assemblyIdentity
          name="ContosoOutlookAddIn"
          version="1.0.0.0"
          language="neutral"
          processorArchitecture="msil" />
      </vstav3:entryPoint>
    </vstav3:entryPoints>
  </vstav3:entryPointsCollection>
```

## <a name="multi-project-deployment-example"></a>複数プロジェクトの配置の例

### <a name="description"></a>説明
 次のコード例では、2 つの Office ソリューションを使用した複数プロジェクトの配置でのアプリケーション マニフェストにある `entryPointsCollection` 要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:entryPointsCollection>
      <vstav3:entryPoints
        id="ContosoExcel">
        <vstav3:entryPoint
          class="ContosoExcelWorkbook.ThisWorkbook">
          <assemblyIdentity
            name="ContosoExcelWorkbook"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:entryPoint
          class="ContosoExcelWorkbook.Sheet1">
          <assemblyIdentity
            name="ContosoExcelWorkbook"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:entryPoint
          class="ContosoExcelWorkbook.Sheet2">
          <assemblyIdentity
            name="ContosoExcelWorkbook"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
        <vstav3:entryPoint
          class="ContosoExcelWorkbook.Sheet3">
          <assemblyIdentity
            name="ContosoExcelWorkbook"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
      </vstav3:entryPoints>
      <vstav3:entryPoints
        id="ContosoOutlook">
        <vstav3:entryPoint
          class="ContosoOutlookAddIn.ThisAddIn">
          <assemblyIdentity
            name="ContosoOutlookAddIn"
            version="1.0.0.0"
            language="neutral"
            processorArchitecture="msil" />
        </vstav3:entryPoint>
      </vstav3:entryPoints>
    </vstav3:entryPointsCollection>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)