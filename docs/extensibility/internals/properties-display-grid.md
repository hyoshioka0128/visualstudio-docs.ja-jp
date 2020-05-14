---
title: プロパティ表示グリッド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d094c32ba8a64fc636f3fb6dfb2944dc3955628a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706190"
---
# <a name="properties-display-grid"></a>プロパティ表示グリッド

**[プロパティ]** ウィンドウには、グリッド内にフィールドが表示されます。 左側の列にはプロパティ名が含まれます。右側の列にはプロパティ値が含まれます。

## <a name="work-with-the-grid"></a>グリッドの操作

2 列のリストには、構成に依存しないプロパティが、デザイン時に変更できるプロパティとその現在の設定が表示されます。 すべてのプロパティが表示されない場合があることに注意してください。 プロパティは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>たとえばメソッドを実装することによって非表示として設定できます。 具体的には、子プロパティを持つプロパティを非表示にするには、

1. パラメーターを`pfDisplay`に<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A>`FALSE`設定します。

2. パラメーターを`pfHide`に<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A>`TRUE`設定します。

情報を **[プロパティ]** ウィンドウにプッシュするには<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>、 IDE で を使用します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>は、**プロパティ**ウィンドウに表示される関連するプロパティを持つ選択可能なオブジェクトを含む各ウィンドウの VSPackages によって呼び出されます。 **ソリューション エクスプローラ**の__VSHPROPIDを<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>使用`GetProperty`した呼び出しの実装[。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)プロジェクト階層で、階層内の参照可能オブジェクトを取得します。

VSPackage が__VSHPROPIDをサポートしていない場合[。VSHPROPID_BrowseObject、IDE](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)は __VSHPROPID<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>の値を使用して使用しようとします[。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>)階層品目が供給するVSHPROPID_SelContainer。

プロジェクト VSPackage を実装する<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>IDE 提供のウィンドウ パッケージ (たとえば、**ソリューション エクスプローラー**) が<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>作成する必要はありません。

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>IDE によって呼び出される 3 つのメソッドで構成されます。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A>**には、[プロパティ]** ウィンドウに表示されるように選択したオブジェクトの数が含まれます。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>プロパティ`IDispatch`ウィンドウに表示されるように選択されているオブジェクトを返**Properties**します。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A>を使用すると、返される<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>オブジェクトがユーザーによって選択されます。 これにより、VSPackage は、UI でユーザーに表示される選択を視覚的に更新できます。

**[プロパティ]** ウィンドウは、オブジェクト`IDispatch`から情報を抽出して、参照するプロパティを取得します。 プロパティ ブラウザは`IDispatch`、 から`IDispatch::GetTypeInfo`取得した クエリを実行して、`ITypeInfo`オブジェクトに対してサポートするプロパティを確認するために使用します。 ブラウザーは、これらの値を使用して **[プロパティ]** ウィンドウにデータを設定し、グリッドに表示される個々のプロパティの値を変更します。 プロパティ情報は、オブジェクト自体の内部で維持されます。

返されるオブジェクトは`IDispatch`サポートされるので、呼び`IDispatch::Invoke``ITypeInfo::Invoke`出し元は、オブジェクト名などの情報を取得できます。 宣言された DSPIID は、ユーザー定義の識別子と競合しないように、負の値です。

**[プロパティ]** ウィンドウには、選択したオブジェクトの特定のプロパティの属性に応じて、さまざまな種類のフィールドが表示されます。 これらのフィールドには、編集ボックス、ドロップダウン リスト、カスタム エディター ダイアログ ボックスへのリンクが含まれます。

- 列挙されたリストに含まれる値は、 への<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>`IDispatch`クエリによって取得されます。 列挙されたリストから取得した値は、フィールド名をダブルクリックするか、値をクリックしてドロップダウン リストから新しい値を選択することにより、プロパティ グリッドで変更できます。 列挙されたリストから設定が事前定義されているプロパティの場合は、[プロパティ] ボックスの一覧でプロパティ名をダブルクリックすると、選択できる項目が順に表示されます。 true/false など、2 つの選択肢のみを持つ定義済みのプロパティの場合は、プロパティ名をダブルクリックして選択を切り替えます。

- の<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A>場合`false`、値が変更されたことを示す値は太字で表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A>は、値を元の値にリセットできるかどうかを判断するために使用されます。 その場合は、値を右クリックして表示されるメニューから **[リセット**] を選択することで、既定値に戻すことができます。 それ以外の場合は、手動で値をデフォルトに戻す必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>また、デザイン時に表示されるプロパティの名前をローカライズおよび非表示にすることもできますが、実行時に表示されるプロパティ名には影響しません。

- 省略記号 (..) ボタンをクリックすると、ユーザーが選択できるプロパティ値のリストが表示されます (カラー ピッカーやフォント リストなど)。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder>これらの値を指定します。

## <a name="see-also"></a>関連項目

- [プロパティを拡張する](../../extensibility/internals/extending-properties.md)
