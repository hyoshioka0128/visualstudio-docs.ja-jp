---
title: Excel 用にコード化された UI テストの拡張機能のサンプル | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- coded UI tests, extensions for Excel
ms.assetid: 451e4d14-7fac-42f9-af56-2bdc8414c6c7
caps.latest.revision: 15
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e0c6075f9f95f7dc1d21db91936cf35c76f9b2e5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672227"
---
# <a name="sample-coded-ui-test-extension-for-excel"></a>Excel 用にコード化された UI テストの拡張子のサンプル
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプルの拡張機能コンポーネントは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のコード化された UI テスト プロセスで実行され、`ExtensionPackage` クラスをベースにして多少階層的になります。 コントロール要素が最上位レベルで、`TechnologyManager` クラス、`ActionFilter` クラス、および `PropertyProvider` クラスはその次のレベルにあります。

 ![Excel テスト拡張機能のアーキテクチャ](../test/media/excel-extarch.png "Excel_ExtArch") Excel 拡張機能のアーキテクチャ

## <a name="extension-points"></a>拡張ポイント
 これらのクラスはサンプルに実装される拡張ポイントを表し、[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 用のコード化された UI テストを可能にします。

### <a name="extensionpackage"></a>ExtensionPackage
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage> から継承されます。これはコード化された UI テスト拡張機能のエントリ ポイントです。 この抽象クラスを実装すると、コード化された UI テスト フレームワークが、新しい UI をテストするために、カスタム UI テスト テクノロジ マネージャー、UI テスト プロパティ プロバイダー、および UI テスト アクション フィルターに内部アクセスできるようになります。 詳細については、「[ExtensionPackage Class (ExtensionPackage クラス)](../test/sample-excel-extension-extensionpackage-class.md)」を参照してください。

### <a name="technologymanager"></a>TechnologyManager
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> クラスから継承されます。このクラスには、テスト記録および再生用のテクノロジ マネージャーが用意されています。 詳細については、「[TechnologyManager Class (TechnologyManager クラス)](../test/sample-excel-extension-technologymanager-class.md)」を参照してください。

### <a name="actionfilter"></a>ActionFilter
 このクラスは、 [Uitestactionfilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110)) クラスから継承され、類似したテストアクションの結果を単一のテスト結果に集約するための基本クラスを提供します。 詳細については、「[ActionFilter Class (ActionFilter クラス)](../test/sample-excel-extension-actionfilter-class.md)」を参照してください。

### <a name="technology-elements"></a>テクノロジ要素
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> クラスから継承された基底クラスには、UI テストで記録および再生に使用できるテクノロジ要素の基礎が用意されています。 詳細については、「[Element Classes (要素クラス)](../test/sample-excel-extension-element-classes.md)」を参照してください。

### <a name="propertyprovider"></a>PropertyProvider
 <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> クラスから継承されます。このクラスには、テスト記録および再生に使用できる UI 要素のプロパティをサポートする基底クラスがあります。 詳細については、「[PropertyProvider Class (PropertyProvider クラス)](../test/sample-excel-extension-propertyprovider-class.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [ExtensionPackage クラス](../test/sample-excel-extension-extensionpackage-class.md)
- [TechnologyManager クラス](../test/sample-excel-extension-technologymanager-class.md)
- [ActionFilter クラス](../test/sample-excel-extension-actionfilter-class.md)
- [Element クラス](../test/sample-excel-extension-element-classes.md)
- [PropertyProvider クラス](../test/sample-excel-extension-propertyprovider-class.md)
