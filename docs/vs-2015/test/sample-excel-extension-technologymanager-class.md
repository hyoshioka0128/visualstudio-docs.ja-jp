---
title: 'Excel 拡張機能のサンプル: TechnologyManager クラス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 8a7b760d-b5ac-4451-9593-6ac1a0b95cdb
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac9a4517fcf13dbb0e1d7a6f994092168723e660
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672151"
---
# <a name="sample-excel-extension-technologymanager-class"></a>Excel 拡張子のサンプル: TechnologyManager クラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このクラスは <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> クラスを拡張します。また、[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 拡張機能用のコア サービスを提供する役割があります。 基底クラスには多くのメソッドがありますが、このサンプルではそのサブセットのみを使用します。

 一部のメソッドは単にプロパティ値を返します。 多くのメソッドは、コード化された UI テスト エンジンに組み込まれている既定のアルゴリズムを開発者がオーバーライドできるように用意されています。 これらのメソッドは、<xref:System.NotSupportedException> をスローするか、`null` を返して、既定のアルゴリズムを使用するようフレームワークに指示します。

 基になるテクノロジの複雑さに応じて、テクノロジ マネージャー コードの開発には数週間から数か月かかる場合があります。 Excel を使用すると、非常に広範なテクノロジ マネージャーを作成することが可能になります。 この例では、意図的に Excel のワークシートとセルだけに限定し、使用する書式設定も制限しています。

 可能であれば、テクノロジ マネージャー コードは `Communicator` クラスによって開かれた .NET リモート処理チャネルを使用し、Excel プロセスで実行されているアドインから情報を抽出します。

## <a name="com-visibility"></a>COM の参照範囲
 このクラスと、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> クラスを拡張する各要素クラスにはいずれも値が `true` の <xref:System.Runtime.InteropServices.ComVisibleAttribute> があるため、COM からクラスを参照できます。

## <a name="technologyname-property"></a>TechnologyName プロパティ
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.TechnologyName%2A?displayProperty=fullName> プロパティのこのオーバーライドでは、拡張機能の他のコンポーネントについて基礎となるテクノロジを識別できる一意でわかりやすい名前を指定する必要があります。 この拡張機能では、値は "Excel" です。

## <a name="getcontrolsupportlevel-method"></a>GetControlSupportLevel メソッド
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetControlSupportLevel%2A?displayProperty=fullName> メソッドのこのオーバーライドは、指定されたハンドルで表されているコントロールにテクノロジ マネージャーが提供できるサポートのレベルを示す数値を返します。 戻り値が大きくなるほど、コントロールに対するテクノロジ マネージャーのサポート レベルは高くなります。 この場合、メソッドはコントロールが含まれているウィンドウを確認し、それが Excel ワークシートであれば、最も高い値を返します。それ以外の場合はゼロが返され、サポートされないことを表します。

## <a name="methods-to-get-an-element"></a>要素を取得するメソッド
 テクノロジに固有の要素を取得するために、コード化された UI テスト フレームワークによって使用される、いくつかの重要なメソッドがあります。要素を取得するには、ハンドル、画面上のポイント、または別のテクノロジの要素を指定します。 これらのメソッドのコードは、自己記述的です。 基本メソッドは次のとおりです。

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetFocusedElement%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromPoint%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromWindowHandle%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.GetElementFromNativeElement%2A?displayProperty=fullName>

- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.ConvertToThisTechnology%2A?displayProperty=fullName>

## <a name="parsequeryid-method"></a>ParseQueryId メソッド
 コード化された UI テストの作成時に、ユーザーはテストの一部またはすべてのコントロールのプロパティ値を指定できます。 これらのプロパティ値は、テスト フレームワークによって、検索プロパティ (テスト中に特定の UI コントロールを見つけるために使用される、名前と値の組) を作成するために使用されます。 すべての検索プロパティは、各コントロールを含め、テクノロジ内の各要素の <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A?displayProperty=fullName> プロパティの値を表しています。 テストの実行中にコントロールを数回検索しなければならない場合があるため、このメソッドはテクノロジ マネージャーによる特定のコントロールの検索プロパティの解析を最適化できるようにします。 またこのメソッドは、フレームワークがそのコントロールを後で検索するときに使用できるクッキーも返します。 メソッドのこの実装では、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.AndCondition.Match%2A?displayProperty=fullName> メソッドを使用して検索プロパティを解析します。

## <a name="matchelement-method"></a>MatchElement メソッド
 テクノロジ マネージャーでコントロール検索を実行するには、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.Search%2A?displayProperty=fullName> メソッドを実装して、一致する候補の配列を返すか、<xref:System.NotSupportedException> をスローすることができます。この場合、フレームワークが独自の検索アルゴリズムを使用していることがわかります。 いずれの方法でも、この実装が <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.AndCondition.Match%2A?displayProperty=fullName> メソッドを使用する場所に <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager.MatchElement%2A> メソッドを実装する必要があります。

## <a name="navigation-methods"></a>ナビゲーション メソッド
 これらのメソッドは、指定された要素の親、子、兄弟などを UI 階層から取得します。 コードは単純で、わかりやすいコメントが付けられています。

## <a name="getexcelelement-internal-method"></a>GetExcelElement 内部メソッド
 この内部メソッドは、ウィンドウ ハンドルと Excel 要素についての情報を受け取り、要求された Excel 要素を返します。

## <a name="see-also"></a>参照
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyManager> <xref:System.NotSupportedException>
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
 <xref:System.Runtime.InteropServices.ComVisibleAttribute>
 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A>
 [コード化された UI テストと操作の記録を拡張して Microsoft Exce をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
