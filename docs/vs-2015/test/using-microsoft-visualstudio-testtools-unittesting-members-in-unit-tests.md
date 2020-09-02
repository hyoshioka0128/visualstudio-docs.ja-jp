---
title: 単体テストでの Microsoft.VisualStudio.TestTools.UnitTesting のメンバーの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 0fa335fd-e442-448f-913f-25a19df90a93
caps.latest.revision: 8
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e8b3ea10b96a63bd18098030dc884ac3f3383353
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657183"
---
# <a name="using-microsoftvisualstudiotesttoolsunittesting-members-in-unit-tests"></a>単体テストでの Microsoft.VisualStudio.TestTools.UnitTesting のメンバーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
単体テスト フレームワークは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] での単体テストをサポートしています。 単体テストをコーディングするときに、<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 名前空間のクラスとメンバーを使用します。 単体テストを最初から記述した場合、またはテスト中のコードから生成された単体テストを改良している場合、これらを使用することができます。

## <a name="groups-of-elements"></a>要素のグループ
 単体テスト フレームワークの概要をより明確に説明するために、このセクションでは UnitTesting 名前空間の要素を関連する機能のグループごとにまとめています。

> [!NOTE]
> 名前が文字列 Attribute で終わる Attribute 要素は、使用するときに文字列 Attribute を付けても付けなくてもかまいません。 たとえば、次の 2 つのコード例は同じように機能します。
>
> `[TestClass()]`
>
> `[TestClassAttribute()]`

### <a name="elements-used-for-data-driven-testing"></a>データ ドリブン テストで使用する要素
 データ ドリブン単体テストを設定するには、次の要素を使用します。 詳細については、「[方法: データ ドリブン単体テストを作成する](../test/how-to-create-a-data-driven-unit-test.md)」および「[チュートリアル : データ ソースを定義するための構成ファイルの使用](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)」を参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataAccessMethod>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElement>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElementCollection>

## <a name="attributes-used-to-establish-a-calling-order"></a>呼び出し順序を確立するために使用する属性
 次のいずれかの属性で装飾されたコード要素は、指定した時点で呼び出されます。 詳細については、「 [単体テストの構造](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)」を参照してください。

### <a name="for-assemblies"></a>アセンブリの場合
 AssemblyInitialize がアセンブリの読み込みの直後に、AssemblyCleanup がアセンブリのアンロードの直前に呼び出されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyCleanupAttribute>

### <a name="for-classes"></a>クラスの場合
 ClassInitialize がクラスの読み込みの直後に、ClassCleanup がクラスのアンロードの直前に呼び出されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassCleanupAttribute>

### <a name="for-test-methods"></a>テスト メソッドの場合

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>

## <a name="attributes-used-to-identify-test-classes-and-methods"></a>テスト クラスとテスト メソッドの識別に使用する属性
 各テスト クラスには TestClass 属性が必要であり、各テスト メソッドには TestMethod 属性が必要です。 詳細については、「 [単体テストの構造](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)」を参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>

## <a name="assert-classes-and-related-exceptions"></a>Assert クラスおよび関連する例外
 単体テストでは、さまざまな種類の Assert のステートメント、例外、属性を使用することで、特定のアプリケーションの動作を確認できます。 詳細については、「[Assert クラスの使用](../test/using-the-assert-classes.md)」を参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute>

## <a name="the-testcontext-class"></a>TestContext クラス
 次の属性とそれらに割り当てられた値は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で、特定のテスト メソッドの [プロパティ] ウィンドウに表示されます。 これらの属性は、単体テストのコードからアクセスするためのものではありません。 代わりに、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の IDE、または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] テストエンジンのいずれかによる単体テストの使用法または実行方法に影響します。たとえば、これらの属性には、[テスト マネージャー] ウィンドウや [テスト結果] ウィンドウの列として表示されるものがあり、それらを使用してテストやテスト結果をグループ化したり並べ替えたりできます。 このような属性の 1 つに TestPropertyAttribute があります。この属性を使用して、任意のメタデータを単体テストに追加できます。 たとえば、これを使用し、単体テストを `[TestProperty("TestPass", "Accessibility")]` とマークして、このテストの対象となるテスト パスの名前を格納できます。 または、`[TestProperty("TestKind", "Localization")]` を使用して、テストの種類のインジケーターを格納できます。 この属性を使用して作成するプロパティ、および割り当てるプロパティ値は、どちらも [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の [プロパティ] ウィンドウの **[各テストで特有]** という見出しの下に表示されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DescriptionAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.WorkItemAttribute>

## <a name="test-configuration-classes"></a>テスト構成クラス

- [ObjectTypes](/previous-versions/visualstudio/visual-studio-2013/dd987428(v=vs.120))

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection>

## <a name="attributes-used-for-generating-reports"></a>レポートの生成に使用する属性
 このセクションの属性は、それらの属性が装飾するテスト メソッドを [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] チーム プロジェクトのプロジェクト階層内のエンティティに関連付けます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssIterationAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssProjectStructureAttribute>

## <a name="classes-used-with-private-accessors"></a>プライベート アクセサーと共に使用するクラス
 「[publicize を使用したプライベート アクセサーの作成](https://msdn.microsoft.com/2056c6a7-6672-42a7-8f53-fead33c56deb)」に説明されているように、プライベート メソッドの単体テストを生成できます。 生成するとプライベート アクセサー クラスが作成され、このクラスにより、PrivateObject クラスのオブジェクトがインスタンス化されます。 PrivateObject クラスは、プライベート アクセサー プロセスの一部としてリフレクションを使用するラッパー クラスです。 これは PrivateType クラスに似ていますが、PrivateType クラスは、プライベート インスタンス メソッドの呼び出しではなく、プライベート静的メソッドの呼び出しに使用されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType>

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>