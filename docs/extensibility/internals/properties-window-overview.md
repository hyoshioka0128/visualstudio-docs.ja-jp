---
title: '[プロパティ] ウィンドウの概要 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window
ms.assetid: 289ed4f2-02ac-4899-855e-42dfe57ee05f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 445a43cec976f363873c89dfe9b8e05429aebaf2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706029"
---
# <a name="properties-window-overview"></a>プロパティ ウィンドウの概要
「**プロパティー」** ウィンドウは、統合開発環境 (IDE) で使用可能な 2 つの主要[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]なタイプのウィンドウで選択されたオブジェクトのプロパティを表示するために使用します。 次の 2 種類のウィンドウがあります。

- ソリューション エクスプローラー、クラス ビュー、オブジェクト ブラウザーなどのツール ウィンドウ

- フォーム デザイナ、XML エディタ、および HTML エディタとして、このようなエディタやデザイナを含むドキュメント ウィンドウ

## <a name="using-the-properties-window"></a>[プロパティ] ウィンドウの使用
 **[プロパティ]** ウィンドウには、1 つまたは複数の選択項目のプロパティが表示されます。 複数のアイテムを選択した場合は、選択したすべてのオブジェクトのすべてのプロパティの交差部分が表示されます。

 フォーム デザイン ウィンドウまたは COM+ メタデータを使用した HTML エディター内で選択されたオブジェクトに関連するイベントが **、[プロパティ]** ウィンドウに表示されます。 たとえば、ボタンを選択し、そのボタンにリンクできる`OnClick`イベントなどの関連イベントを表示できます。

 **[プロパティ]** ウィンドウに表示されるイベントは、主にコードにバインドされたオブジェクトで使用されます。 コードとは関係のないファイル形式を編集する場合は、イベントを持つ必要はありません。 イベントは、実行中のコードと特定のオブジェクトに関連付けられた特定のイベントとの間にバインディングがある場合にのみ **、[プロパティ]** ウィンドウに表示されます。 この例としては、選択したオブジェクトの背後にあるコードが、そのオブジェクトがアクティブになったときに実行されるコードが挙されます。

 次の表は、[**プロパティ]** ウィンドウで使用される主要なインターフェイスの一覧です。

|Interface Name|説明|
|--------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties>|**[プロパティ]** ウィンドウにカテゴリの一覧を表示し、各プロパティをカテゴリにマップします。|
|[I ディスパッチ インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)|オートメーションをサポートするプログラミング ツールやその他のアプリケーションにオブジェクトのメソッドとプロパティを公開します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>|オブジェクト自体によって実装されたモーダル ダイアログ ウィンドウを開く *、ビルダー*と呼ばれる省略記号 (..) ボタンを提供します。 ユーザーがテキスト フィールドに値を入力しにくい場合に使用します。 たとえば、RGB 値を決定するカラー ピッカーを開くために使用できます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>|**[プロパティ]** ウィンドウに表示される情報を更新するために使用するオブジェクトへのアクセスを提供します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>は、表示する関連プロパティを持つ選択可能なオブジェクトを含む各ウィンドウの VSPackages によって実装されます。|
|<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>|インターフェイスのメソッドや構造体のフィールドなど、オブジェクトの型に関する情報を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|VSPackages が選択イベントの通知を受信し、現在のプロジェクト階層、項目、要素値、およびコマンド UI コンテキストに関する情報を取得できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiItemSelect>|複数の選択項目にアクセスできる環境を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>|**[プロパティ]** ウィンドウに表示される一部のプロパティにローカライズされた名前を指定するために使用します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents>|現在の選択、要素値、またはコマンド UI コンテキストに対する変更を登録 VSPackage に通知します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|現在の選択項目の変更を環境に通知し、新しい選択に関連する階層情報および明細情報へのアクセスを提供します。|

 の詳細については`IDispatch`、MSDN ライブラリを参照してください。

## <a name="see-also"></a>関連項目
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
- [プロパティ ウィンドウのフィールドとインターフェイス](../../extensibility/internals/properties-window-fields-and-interfaces.md)
