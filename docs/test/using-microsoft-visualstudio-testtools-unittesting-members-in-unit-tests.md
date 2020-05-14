---
title: 単体テストで Microsoft.VisualStudio.TestTools.UnitTesting を使用する
ms.date: 03/02/2018
ms.topic: reference
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: e45df63f36947b5f6f0aad77bb8eebcab4aca731
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585562"
---
# <a name="use-the-mstest-framework-in-unit-tests"></a>単体テストでの MSTest フレームワークの使用

[MSTest](<xref:Microsoft.VisualStudio.TestTools.UnitTesting>) フレームワークは、Visual Studio での単体テストをサポートしています。 単体テストをコーディングするときに、<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 名前空間のクラスとメンバーを使用します。 コードから生成された単体テストを調整するときにも、それらを使用できます。

## <a name="framework-members"></a>フレームワークのメンバー

単体テスト フレームワークの概要をより明確に説明するために、このセクションでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 名前空間のメンバーを関連する機能グループごとにまとめています。

> [!NOTE]
> 名前が "Attribute" で終わる属性要素は、使用するときに末尾に "Attribute" を付けても付けなくてもかまいません。 たとえば、次の 2 つのコード例は同じように機能します。
>
> `[TestClass()]`
>
> `[TestClassAttribute()]`

### <a name="members-used-for-data-driven-testing"></a>データ ドリブン テストで使用する要素

データ ドリブン単体テストを設定するには、次の要素を使用します。 詳細については、「[データ ドリブン単体テストを作成する](../test/how-to-create-a-data-driven-unit-test.md)」および「[データ ソースを定義するための構成ファイルの使用](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)」を参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataAccessMethod>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElement>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceElementCollection>

## <a name="attributes-used-to-establish-a-calling-order"></a>呼び出し順序を確立するために使用する属性

次のいずれかの属性で装飾されたコード要素は、指定した時点で呼び出されます。 詳細については、「[単体テストの構造](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)」を参照してください。

### <a name="attributes-for-assemblies"></a>アセンブリの属性

AssemblyInitialize がアセンブリの読み込みの直後に、AssemblyCleanup がアセンブリのアンロードの直前に呼び出されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssemblyCleanupAttribute>

### <a name="attributes-for-classes"></a>クラスの属性

ClassInitialize がクラスの読み込みの直後に、ClassCleanup がクラスのアンロードの直前に呼び出されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ClassCleanupAttribute>

### <a name="attributes-for-test-methods"></a>テスト メソッドの属性

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestInitializeAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCleanupAttribute>

## <a name="attributes-used-to-identify-test-classes-and-methods"></a>テスト クラスとテスト メソッドの識別に使用する属性

すべてのテスト クラスには `TestClass` 属性が必要であり、すべてのテスト メソッドには `TestMethod` 属性が必要です。 詳細については、「[単体テストの構造](https://msdn.microsoft.com/a03d1ee7-9999-4e7c-85df-7d9073976144)」を参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute>

## <a name="assert-classes-and-related-exceptions"></a>Assert クラスおよび関連する例外

単体テストでは、さまざまな種類のアサーション、例外、および属性を使用して、特定のアプリケーションの動作を確認できます。 詳細については、[Assert クラスの使用](../test/using-the-assert-classes.md)に関するページを参照してください。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException>

## <a name="the-testcontext-class"></a>TestContext クラス

次の属性とそれらに割り当てられた値は、Visual Studio Properties で特定のテスト メソッドの [プロパティ] ウィンドウに表示されます。 これらの属性は、単体テストのコードからアクセスするためのものではありません。 代わりに、Visual Studio の IDE、または Visual Studio テスト エンジンのいずれかによる単体テストの使用法または実行方法に影響します。 たとえば、これらの属性には、 **[テスト マネージャー]** ウィンドウや **[テスト結果]** ウィンドウの列として表示されるものがあり、それらを使用してテストやテスト結果をグループ化したり並べ替えたりできます。 このような属性の 1 つに <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute> があります。この属性を使用して、任意のメタデータを単体テストに追加できます。 たとえば、これを使用し、単体テストを `[TestProperty("TestPass", "Accessibility")]` とマークして、このテストの対象となるテスト パスの名前を格納できます。 または、`[TestProperty("TestKind", "Localization")]` を使用して、テストの種類のインジケーターを格納できます。 この属性を使用して作成するプロパティ、および割り当てるプロパティ値は、どちらも Visual Studio の **[プロパティ]** ウィンドウの **[各テストで特有]** という見出しの下に表示されます。

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

## <a name="attributes-used-to-generate-reports"></a>レポートの生成に使用される属性

このセクションの属性は、それらの属性が装飾するテスト メソッドを Team Foundation Server チーム プロジェクトのプロジェクト階層内のエンティティに関連付けます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssIterationAttribute>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.CssProjectStructureAttribute>

## <a name="classes-used-with-private-accessors"></a>プライベート アクセサーと共に使用するクラス

プライベート メソッドの単体テストを生成できます。 生成するとプライベート アクセサー クラスが作成され、このクラスにより、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject> クラスのオブジェクトがインスタンス化されます。 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject> クラスは、プライベート アクセサー プロセスの一部としてリフレクションを使用するラッパー クラスです。 これは <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType> クラスに似ていますが、PrivateType クラスは、プライベート インスタンス メソッドの呼び出しではなく、プライベート静的メソッドの呼び出しに使用されます。

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateObject>

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.PrivateType>

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>リファレンス ドキュメント
