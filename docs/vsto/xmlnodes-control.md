---
title: XMLNodes コントロール
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, events
- XMLNodes control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9ad16165924a33a25dab2b1cfb49a0a7bbfe0875
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842262"
---
# <a name="xmlnodes-control"></a>XMLNodes コントロール
  **重要** このトピックに記載されている Microsoft Word に関する情報は、microsoft word のカスタム XML に関連する特定の機能の実装が microsoft によって削除されたときに、マイクロソフトが2010年1月より前にマイクロソフトによってライセンスされた Microsoft Word 製品米国の特典と使用についてのみ提供されます。 Microsoft Word に関するこの情報は、マイクロソフトが2010年1月10日以降にライセンスを取得した microsoft Word 製品を使用しているか、microsoft Word 製品で実行されているプログラムを開発している個人または米国組織によって読み取られたり使用されたりすることはできません。これらの製品は、その日より前にライセンスされている製品と同じように動作しないか、米国の外部で使用するために購入およびライセンス供与されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNodes>コントロールは、イベントを公開する、マップされた XML ノードオブジェクトのコレクションです。 この <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールは、繰り返しスキーマ要素が Microsoft Office Word 文書にマップされている場合にのみ作成されます。 繰り返し要素に子要素が含まれている場合は、各子要素もコントロールとして作成され <xref:Microsoft.Office.Tools.Word.XMLNodes> ます。

 Visual Studio によって XML ノードのコレクションが作成された後、Word オブジェクトモデルを走査する必要なく、直接コントロールに対してプログラミングすることができます。 コントロールを削除できるのは、 <xref:Microsoft.Office.Tools.Word.XMLNodes> ドキュメントから要素のマッピングを削除することだけです。

> [!NOTE]
> プロパティを使用してコントロールの子要素にアクセスする場合 <xref:Microsoft.Office.Tools.Word.XMLNodes> <xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A> 、コントロールで <xref:Microsoft.Office.Interop.Word.XMLNode> はなく、オブジェクトを返し <xref:Microsoft.Office.Tools.Word.XMLNode> ます。 詳細については、「 [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

## <a name="bind-data-to-the-control"></a>コントロールにデータをバインドする
 <xref:Microsoft.Office.Tools.Word.XMLNodes>コントロールがデータバインディングをサポートしていません。 これは、コントロールには <xref:Microsoft.Office.Tools.Word.XMLNodes> 複雑なデータバインディング機能がなく、単純なデータバインディングでは繰り返しデータを表すことができないためです。

## <a name="formatting"></a>書式設定
 ドキュメント内のテキストに適用できる書式設定は、コントロールに適用でき <xref:Microsoft.Office.Tools.Word.XMLNodes> ます。

## <a name="events"></a>イベント
 コントロールで使用できるイベント <xref:Microsoft.Office.Tools.Word.XMLNodes> は次のとおりです。

- <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>

## <a name="compare-events"></a>イベントの比較
 ユーザーが特定のコントロールのコンテキスト内でカーソルを移動すると、イベントをキャプチャでき <xref:Microsoft.Office.Tools.Word.XMLNodes> ます。 たとえば、という名前の子コントロールを持ち、次のように <xref:Microsoft.Office.Tools.Word.XMLNodes> `Customer` <xref:Microsoft.Office.Tools.Word.XMLNodes> `Company` `Company` とという名前の2つの子コントロール <xref:Microsoft.Office.Tools.Word.XMLNodes> `CompanyName` を持つという名前のコントロールがあるとし `CompanyRegion` ます。

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 カーソルがノードに移動されたときに操作ウィンドウにコントロールを表示する場合 `Company` 、カーソルがに配置されているかどうかは関係ありません `CompanyName` `CompanyRegion` 。どちらものコンテキスト内にあるため `Company` です。 この場合は、のイベントでコードを記述でき <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> `Company` ます。

 ほとんどの場合、カーソルがコントロールに入ると、 <xref:Microsoft.Office.Tools.Word.XMLNodes> <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> イベントとイベントの両方 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> が発生します。 次の表は、これらのイベントの違いを示しています。

|イベントの選択|ContextEnter イベント|
|------------------|------------------------|
|カーソルが、<xref:Microsoft.Office.Tools.Word.XMLNodes> コレクションのノードの 1 つの内側に置かれると発生します。|カーソルが、ノードのコンテキストの外側の領域から、<xref:Microsoft.Office.Tools.Word.XMLNodes> コレクションのノードの 1 つ、または子孫ノードの内側に置かれると発生します。 つまり、コンテキストが変更されたときにのみ発生し、入れ子になった複数のコントロールに対して発生させることができ <xref:Microsoft.Office.Tools.Word.XMLNodes> ます。|

 たとえば、の外部からにカーソルを移動すると、、、 `Customer` `CompanyName` <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> およびの `Customer` イベント `Company` `CompanyName` が発生します。 その後、からにカーソルを移動する `CompanyName` `CompanyRegion` と、 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> のイベントのみ `CompanyRegion` が発生し `Company` ます。これは、コンテキストがとの両方で同じであるためです `Customer` 。 ドキュメントには複数のノードを含めることができ `Company` ます。 カーソルをあるノードから別のノードに移動した場合、 `CompanyName` `Company` `CompanyName` `Company` コンテキストは同じであるため、 <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> イベントのみが発生します。

 イベントとイベントの間にも、同じ違いがあり <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave> <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect> ます。

## <a name="see-also"></a>こちらもご覧ください
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNode コントロール](../vsto/xmlnode-control.md)
- [方法: Word 文書に XMLNodes コントロールを追加する](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
