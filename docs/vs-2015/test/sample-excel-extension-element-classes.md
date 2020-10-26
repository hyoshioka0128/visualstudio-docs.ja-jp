---
title: 'Excel 拡張機能のサンプル: Element クラス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 7c251098-00aa-49cf-9e37-5717c0c6b3f1
caps.latest.revision: 11
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 21c7777be710f0175708629eb9507b34f0d70be2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660448"
---
# <a name="sample-excel-extension-element-classes"></a>Excel 拡張子のサンプル: 要素クラス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この拡張機能は、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> から派生し、[!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 内の Worksheet コントロールと Cell コントロールを表すクラスを使用します。

 この拡張機能の基本要素は `ExcelElement` です。 `ExcelWorksheetElement` クラスおよび `ExcelCellElement` クラスは、この要素を継承します。

## <a name="element-and-elementinformation-classes"></a>Element クラスと ElementInformation クラス
 `Element` は、Excel 拡張機能のすべてのユーザー インターフェイス要素の基底クラスです。<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement> クラスから継承されます。 `ElementInformation` はサンプルの要素情報クラスの基底クラスであり、メンバーを持ちません。

#### <a name="simple-properties-and-methods"></a>単純なプロパティとメソッド
 これらのメンバーは、`Name` プロパティの値や `ClassName` プロパティの値などの単純な値を返し、コードも明快で読みやすいものです。 一部の値は、`Utility` クラスを使用して返されます。これについては、後で説明します。 その他は、このサンプル拡張機能には関連しないので、`null` を返します。 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A> プロパティという <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.CacheProperties%2A> メソッドの 2 つは他のメンバーよりも興味深いメンバーです。

#### <a name="queryid-property"></a>QueryId プロパティ
 このプロパティは、再生中にコントロールを一意に識別する、プロパティ名と値のペアから成る条件を返します。 開発者は、各派生コントロール クラスのこのプロパティをオーバーライドし、フレームワークが UI 内のコントロールを見つけるために使用できる <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement> オブジェクトを返すようにする必要があります。

#### <a name="cacheproperties-method"></a>CacheProperties メソッド
 このメソッドは、記録処理中にテスト フレームワークによって呼び出され、重要なプロパティのスナップショットを保存するよう要素に指示します。 そうすることで、実際の UI コントロールが画面上に存在しなくなった場合でも、プロパティが使用可能な状態で維持されます。

## <a name="worksheetelement-and-worksheetinformation-classes"></a>WorksheetElement クラスと WorksheetInformation クラス
 `WorksheetElement` クラスはテスト フレームワーク内の Excel ワークシートを表し、`Element` 基底クラスを継承します。 <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ClassName%2A>、<xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.ControlTypeName%2A>、および <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.Name%2A> の 3 つのプロパティはオーバーライドされ、Excel ワークシート オブジェクトに関する特定の情報が提供されます。

 また、<xref:System.Runtime.InteropServices.ComVisibleAttribute> もこのクラスに適用され、COM から参照できるようになります。

 `WorksheetInformation` クラスは Excel ワークシートに関する情報を表します。 `SheetName` プロパティという 1 つのメンバーしかありませんが、このサンプルの場合はそれで十分です。

## <a name="cellelement-and-cellinformation-classes"></a>CellElement クラスと CellInformation クラス
 `CellElement` クラスは Excel のセルを表し、`Element` 基底クラスを継承します。 唯一のオーバーライドされるメンバーは <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement.QueryId%2A> です。これは、セルを識別する `RowIndex` および `ColumnIndex` プロパティを使用する <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement> を返します。

## <a name="utilities-and-excelutilities-classes"></a>Utilities クラスと ExcelUtilities クラス
 内部 `ExcelUtilities` クラスには、テクノロジ名などの定数値や、指定されたウィンドウ ハンドルが Excel ワークシートを表すかどうかを判断するメソッドなどが用意されています。

 `Utilities` クラスには、UI に関するさまざまな情報を返すヘルパー メソッドがあります。 一部のメソッドは、**USER32.DLL** や **OLEACC.DLL** などの外部システム DLL への直接呼び出しを使用して、UI のウィンドウ ハンドルを取得します<strong>。</strong>

## <a name="see-also"></a>参照
 <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.IQueryElement>
 [コード化された UI テストと操作の記録を拡張して Microsoft Exce をサポート](../test/extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel.md)
