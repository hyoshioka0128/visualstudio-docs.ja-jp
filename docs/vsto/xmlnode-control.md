---
title: XMLNode コントロール
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a8bd5c4612b59f909ae623eb4092a209798f98c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62975719"
---
# <a name="xmlnode-control"></a>XMLNode コントロール
  **重要** このトピックに記載されている Microsoft Word に関する情報は、microsoft word のカスタム XML に関連する特定の機能の実装が microsoft によって削除されたときに、マイクロソフトが2010年1月より前にマイクロソフトによってライセンスされた Microsoft Word 製品米国の特典と使用についてのみ提供されます。 Microsoft Word に関するこの情報は、マイクロソフトが2010年1月10日以降にライセンスを取得した microsoft Word 製品を使用しているか、microsoft Word 製品で実行されているプログラムを開発している個人または米国組織によって読み取られたり使用されたりすることはできません。これらの製品は、その日より前にライセンスされている製品と同じように動作しないか、米国の外部で使用するために購入およびライセンス供与されます。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNode>コントロールは、イベントを公開し、データにバインドできる、マップされた XML ノードオブジェクトです。 この <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールは、非繰り返しスキーマ要素が Microsoft Office Word 文書にマップされている場合にのみ作成されます。 Visual Studio によって XML ノードが作成された後は、Word オブジェクトモデルを走査する必要なく、そのノードに対して直接プログラミングできます。

 <xref:Microsoft.Office.Tools.Word.XMLNode>Word で要素のマッピングを削除することによってのみ、コントロールを削除できます。

## <a name="bind-data-to-the-control"></a>コントロールにデータをバインドする
 コントロールは、 <xref:Microsoft.Office.Tools.Word.XMLNode> 単純なデータバインディングをサポートします。 XML ノードは、プロパティを使用してデータソースにバインドする必要があり <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> ます。 バインドされたデータセット内のデータが更新されると、 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールがその変更を反映させます。

## <a name="formatting"></a>書式設定
 オブジェクトに適用できる書式設定は <xref:Microsoft.Office.Interop.Word.XMLNode> 、コントロールに適用でき <xref:Microsoft.Office.Tools.Word.XMLNode> ます。 これには、フォント、下線スタイル、および文字スタイルが含まれます。

## <a name="events"></a>イベント
 次のイベントは <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールに対して利用できます。

- <xref:Microsoft.Office.Tools.Word.XMLNode.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ValidationError>

## <a name="compare-events"></a>イベントの比較
 ユーザーが特定のコントロールのコンテキスト内でカーソルを移動すると、イベントをキャプチャでき <xref:Microsoft.Office.Tools.Word.XMLNode> ます。 たとえば、という名前の子コントロールを持ち、次のように <xref:Microsoft.Office.Tools.Word.XMLNode> `Customer` <xref:Microsoft.Office.Tools.Word.XMLNode> `Company` `Company` とという名前の2つの子コントロール <xref:Microsoft.Office.Tools.Word.XMLNode> `CompanyName` を持つという名前のコントロールがあるとし `CompanyRegion` ます。

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 カーソルがノードに移動されたときに操作ウィンドウにコントロールを表示する場合 `Company` 、カーソルがに配置されているかどうかは関係ありません `CompanyName` `CompanyRegion` 。どちらものコンテキスト内にあるため `Company` です。 この場合は、のイベントでコードを記述でき <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `Company` ます。

 ほとんどの場合、カーソルがコントロールに入ると、 <xref:Microsoft.Office.Tools.Word.XMLNode> <xref:Microsoft.Office.Tools.Word.XMLNode.Select> イベントとイベントの両方 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> が発生します。 次の表は、これらのイベントの違いを示しています。

|イベントの選択|ContextEnter イベント|
|------------------|------------------------|
|カーソルが内に置かれたときに発生し <xref:Microsoft.Office.Tools.Word.XMLNode> ます。|ポインターが <xref:Microsoft.Office.Tools.Word.XMLNode> またはその子孫ノードの内部に、ノードのコンテキスト外から配置されたときに発生します。 つまり、コンテキストが変更された場合にのみ発生します。|

 たとえば、の外部からにカーソルを移動すると、、 `Customer` `CompanyName` <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `Customer` 、およびのイベント `Company` `CompanyName` が発生します。 その後、からにカーソルを移動する `CompanyName` `CompanyRegion` と、 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `CompanyRegion` との両方のコンテキスト内にあるため、のイベントのみが発生し `Company` `Customer` ます。

 イベントとイベントの間には、同じ違いがあり <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave> <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect> ます。

## <a name="see-also"></a>こちらもご覧ください
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNodes コントロール](../vsto/xmlnodes-control.md)
- [方法: Word 文書に XMLNode コントロールを追加する](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
