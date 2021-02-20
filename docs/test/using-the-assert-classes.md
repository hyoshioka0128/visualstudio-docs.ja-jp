---
title: MSTest の Assert クラスおよびメソッド
description: Assert ステートメントを使用して、アプリケーション コードの単体テスト中にコードの動作が正しいかどうかをテストする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/07/2018
ms.topic: reference
helpviewer_keywords:
- Assert classes
- Assert methods
- unit tests, Assert classes
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 1f064ee1ca41aab19e19fa6006d983a76ed006d7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99946203"
---
# <a name="use-assert-classes-for-unit-testing"></a>単体テストに Assert クラスを使用する

<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 名前空間の Assert クラスは、特定の機能を確認するために使用します。 単体テスト メソッドはアプリケーション コード内のメソッドのコードを実行しますが、Assert ステートメントを含める場合にのみコードの動作の正確性を報告します。

## <a name="kinds-of-asserts"></a>Assert の種類

<xref:Microsoft.VisualStudio.TestTools.UnitTesting> 名前空間には複数の Assert クラスが用意されています。

テスト メソッドでは、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName> クラスの任意のメソッド (<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=nameWithType> など) を呼び出すことができます。 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> クラスには、多くの選択可能なメソッドがあり、それらのメソッドの多くには複数のオーバーロードが存在します。

### <a name="compare-strings-and-collections"></a>文字列とコレクションを比較する

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.CollectionAssert> クラスは、オブジェクトのコレクションを比較する場合や、コレクションの状態を確認する場合に使用します。

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert> クラスは、文字列の比較と確認に使用します。 このクラスには、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=nameWithType>、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Matches%2A?displayProperty=nameWithType>、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.StartsWith%2A?displayProperty=nameWithType> などのさまざまな便利なメソッドがあります。

### <a name="exceptions"></a>例外

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertFailedException> 例外は、テストが失敗するたびにスローされます。 タイムアウトした場合、予期しない例外がスローされた場合、または **失敗** の結果を出力する Assert ステートメントを含む場合、テストは失敗します。

<xref:Microsoft.VisualStudio.TestTools.UnitTesting.AssertInconclusiveException> は、テストで **結果不確定** の結果が出力されるたびにスローされます。 通常、まだ編集中のテストに対して、そのテストを実行する準備ができていないことを示すために <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Inconclusive%2A?displayProperty=nameWithType> ステートメントを追加します。

> [!NOTE]
> 別の方法として、実行の準備が整っていないテストに <xref:Microsoft.VisualStudio.TestTools.UnitTesting.IgnoreAttribute> 属性でマークを付けることもできます。 しかし、この方法には、まだ実装していないテストの個数に関するレポートを簡単に生成できないという短所があります。

新しい Assert 例外クラスを記述する場合には、そのクラスに基本クラス <xref:Microsoft.VisualStudio.TestTools.UnitTesting.UnitTestAssertException> から継承させると、例外が発生した場合に、その例外がテストや運用コードからスローされた予期しない例外なのか、アサーションによる失敗なのかを識別しやすくなります。

アプリケーション コード内のあるメソッドによりスローされることが予想される例外が実際にスローされることを確認するには、<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType> メソッドを使用します。

## <a name="see-also"></a>関連項目

- [コードの単体テスト](../test/unit-test-your-code.md)
