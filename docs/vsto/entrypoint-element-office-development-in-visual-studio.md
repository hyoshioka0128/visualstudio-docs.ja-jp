---
title: '&lt;entryPoint &gt; 要素 (Visual Studio での Office 開発)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <entryPoint> element
- <entryPoint> element
- entryPoint element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 17f57b90b7c6aa4c254b2b55ee838a3086193ef7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543599"
---
# <a name="ltentrypointgt-element-office-development-in-visual-studio"></a>&lt;entryPoint &gt; 要素 (Visual Studio での Office 開発)
  `entryPoint` 名前空間の各 `vstav3` 要素によって、この [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] アプリケーションのインストール時に実行する必要のあるカスタマイズ アセンブリを指定します。

## <a name="syntax"></a>構文

```xml
<entryPoint class>
    <assemblyIdentity />
</entryPoint>
```

## <a name="elements-and-attributes"></a>要素と属性
 `entryPoint` 要素は必須です。この要素は `vstav3` 名前空間にあります。

 `entryPoint` 要素ごとに、1 つのカスタマイズ アセンブリのみを含めることができます。 アプリケーション マニフェストには、複数の `entryPoint` 要素を定義できます。

 `entryPoint` 要素には、次の属性があります。

|属性|説明|
|---------------|-----------------|
|`class`|必須。 実行するカスタマイズ アセンブリを指定します。 この属性の構文は、 *NamespaceName.ClassName*です。|

 `entryPoint` には、次の要素があります。

### <a name="assemblyidentity"></a>assemblyIdentity
 必須。 `assemblyIdentity` 名前空間の `vstav3` 要素は、 `assemblyIdentity` アプリケーション マニフェストで定義された既存の [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 要素を参照します。

 `assemblyIdentity`とその属性の役割は、 [ClickOnce アプリケーション&#41;&#40;&#60;assemblyIdentity&#62; 要素](../deployment/assemblyidentity-element-clickonce-application.md)で定義されています。

## <a name="document-level-customization-example"></a>ドキュメントレベルのカスタマイズの例

### <a name="description"></a>説明
 次のコード例は、 `entryPoint` を使用して配置するドキュメント レベルの Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
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
```

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="description"></a>説明
 次のコード例は、 `entryPoint` を使用して配置するアプリケーション レベルの Office ソリューションに対するアプリケーション マニフェストの [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]要素を示しています。 このコード例は、 [Office ソリューションのアプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)に用意されている大規模な例の一部です。

### <a name="code"></a>コード

```xml
<vstav3:entryPoint
  class="ContosoOutlookAddIn.ThisAddIn">
  <assemblyIdentity
    name="ContosoOutlookAddIn"
    version="1.0.0.0"
    language="neutral"
    processorArchitecture="msil" />
</vstav3:entryPoint>
```

## <a name="see-also"></a>関連項目

- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)