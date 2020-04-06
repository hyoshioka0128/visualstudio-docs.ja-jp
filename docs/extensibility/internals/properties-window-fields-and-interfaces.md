---
title: プロパティ ウィンドウのフィールドとインターフェイス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9529708c781e7fdb04c3b4c5ee143b7605857e84
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706159"
---
# <a name="properties-window-fields-and-interfaces"></a>プロパティ ウィンドウのフィールドとインターフェイス
IDE でフォーカスを持つウィンドウに基づいて、[**プロパティ]** ウィンドウに表示される情報を決定するための選択モデル。 選択したウィンドウ内のすべてのウィンドウとオブジェクトは、その選択コンテキストオブジェクトをグローバル選択コンテキストにプッシュできます。 環境は、そのウィンドウにフォーカスがあるときに、ウィンドウ フレームの値を使用してグローバル選択コンテキストを更新します。 フォーカスが変更されると、選択コンテキストも変更されます。

## <a name="tracking-selection-in-the-ide"></a>IDE での選択の追跡
 IDE が所有するウィンドウフレームまたはサイトには、 という<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>サービスがあります。 次の手順では、ユーザーが別の開いているウィンドウにフォーカスを変更するか、**ソリューション エクスプローラー**で別のプロジェクト項目を選択することによって、選択項目の変更を実装して **、[プロパティ]** ウィンドウに表示されるコンテンツを変更する方法を示します。

1. 選択したウィンドウに配置されている VSPackage によって作成されたオブジェクトが呼<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>び出<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>し<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>を行います。

2. 選択したウィンドウによって提供される選択コンテナは、独自<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>のオブジェクトを作成します。 選択が変更されると、VSPackage は<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>、**変更のプロパティ**ウィンドウを含む環境内のすべてのリスナーに通知を呼び出します。 また、新しい選択に関連する階層情報および明細情報へのアクセスも提供します。

3. パラメータ<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>内の選択した階層項目を呼び`VSHPROPID_BrowseObject`出して渡すと<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>、オブジェクトが設定されます。

4. [IDispatch インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)から派生したオブジェクトが__VSHPROPIDに返されます[。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)要求された項目に対して、環境によって、それを に<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>ラップします (次の手順を参照)。 呼び出しが失敗した場合、環境は、`IVsHierarchy::GetProperty`選択コンテナー__VSHPROPIDを渡す 2 回目の呼び出しを行います[。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>)階層品目が供給するVSHPROPID_SelContainer。

    プロジェクト VSPackage は、<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>それを実装する環境が提供するウィンドウ VSPackage (たとえば、**ソリューション エクスプ ローラー**)<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>が代わりに構築するため作成されません。

5. 環境は、**プロパティ**ウィンドウに<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>入力するインターフェイスに基づいてオブジェクト`IDispatch`を取得するメソッドを呼び出します。

   **[プロパティ]** ウィンドウの値が変更されると、VSPackages `IVsTrackSelectionEx::OnElementValueChangeEx` `IVsTrackSelectionEx::OnSelectionChangeEx`は要素値の変更を実装し、変更を報告します。 次に、環境が<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>呼<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>び出されるか **、またはプロパティ**ウィンドウに表示される情報をプロパティ値と同期させて保持します。 詳細については、「[プロパティ ウィンドウでプロパティ値を更新する 」を参照してください](#updating-property-values-in-the-properties-window)。

   **ソリューション エクスプローラー**で別のプロジェクト項目を選択して、その項目に関連するプロパティを表示する以外に、フォームまたはドキュメント ウィンドウ内の別のオブジェクトを**選択**することもできます。 詳細については、「[プロパティ ウィンドウ オブジェクト リスト](../../extensibility/internals/properties-window-object-list.md)」を参照してください。

   **プロパティ**ウィンドウグリッドでの情報の表示方法をアルファベットからカテゴリに変更できます。 **Properties** 詳細については、「[プロパティ ウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md)と[プロパティ ページ](../../extensibility/internals/property-pages.md)」を参照してください。

   最後に、[**プロパティ]** ウィンドウの下部には、[**プロパティ]** ウィンドウ グリッドで選択したフィールドの説明も含まれています。 詳細については、「[プロパティ ウィンドウからのフィールドの説明の取得 」](#getting-field-descriptions-from-the-properties-window)を参照してください。

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a>プロパティ ウィンドウでのプロパティ値の更新
**[プロパティ]** ウィンドウをプロパティ値の変更と同期するには、2 つの方法があります。 1 番目の方法は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを呼び出すことです。このインターフェイスは、環境によって用意されているツール ウィンドウやドキュメント ウィンドウのアクセスや作成を含む、基本的なウィンドウ操作機能へのアクセスを提供します。 次の手順は、この同期プロセスを説明したものです。

### <a name="updating-property-values-using-ivsuishell"></a>IVsUIShell を使ってプロパティ値を更新する

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>IVsUIShell インターフェイスを使ってプロパティ値を更新するには

1. VSPackage、プロジェクト、エディターがツール ウィンドウまたはドキュメント ウィンドウを作成したり列挙したりする必要が生じた時点で、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> を (<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスを通じて) 呼び出します。

2. イベント<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A>を実装<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>および発生<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A>させることなく、プロジェクト (または [**プロパティ]** ウィンドウで参照されているその他の選択したオブジェクト) のプロパティ変更と [**プロパティ]** ウィンドウを同期させる実装。

3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> のメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> を実装します。この 2 つのメソッドは、それぞれ、階層イベントのクライアント通知を設定および無効化します。これにより、階層で <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を実装する必要がなくなります。

### <a name="updating-property-values-using-iconnection"></a>IConnection を使ってプロパティ値を更新する
 **[プロパティ]** ウィンドウとプロパティ値の変更を同期する 2 番目の方法は、接続可能なオブジェクトに `IConnection` を実装することにより、発信インターフェイスの存在を示すことです。 プロパティ名をローカライズする場合は、オブジェクトを <xref:System.ComponentModel.ICustomTypeDescriptor> から派生させます。 <xref:System.ComponentModel.ICustomTypeDescriptor> の実装では、実装から返すプロパティ記述子を変更し、プロパティの名前を変更できます。 説明をローカライズするには、<xref:System.ComponentModel.DescriptionAttribute> から派生させた属性を作成し、Description プロパティをオーバーライドします。

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>IConnection インターフェイスを実装する際の考慮事項

1. `IConnection` は、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを提供します。 また、すべての接続ポイント サブオブジェクトへのアクセスも提供し、それぞれは <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを実装します。

2. すべての参照オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> イベントを実装する必要があります。 **[プロパティ]** ウィンドウは、 `IConnection`を通してイベントを設定することをお勧めします。

3. 接続ポイントは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> の実装で許容される接続数 (1 つまたは複数) を制御します。 インターフェイスを 1 つのみ許容する接続ポイントでは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> メソッドから <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> を返すことができます。

4. クライアントは、`IConnection` インターフェイスを呼び出すことにより、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを取得できます。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを呼び出すと、各発信インターフェイス ID (IID) の接続ポイントを列挙することができます。

5. また、`IConnection` を呼び出すことにより、各発信 IID への <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを持つ接続ポイント サブオブジェクトへのアクセスを取得することもできます。 インターフェイスを<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint>介して、クライアントは接続可能オブジェクトとクライアント自身の同期を使用してアドバイザリ ループを開始または終了します。クライアントは、インターフェイスを<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint>呼び出して、インターフェイスを持つ<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections>列挙子オブジェクトを取得して、認識している接続を列挙することもできます。

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a>[プロパティ] ウィンドウからのフィールドの説明の取得
**[プロパティ]** ウィンドウの下部にある説明領域に、選択したプロパティ フィールドに関連する情報が表示されます。 この機能は既定で有効になっています。 説明フィールドを非表示にするには、 **[プロパティ]** ウィンドウを右クリックし、 **[説明]** をクリックします。 これにより、メニュー ウィンドウの **[説明]** タイトルの横のチェック マークが削除されます。 同じ手順を行って **[説明]** の表示をオンに戻すことにより、フィールドを再度表示できます。

 説明フィールド内の情報は <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> から取得されます。 それぞれのメソッド、インターフェイス、コクラスなどには、タイプ ライブラリのローカライズされていない `helpstring` 属性を適用できます。 **[プロパティ]** ウィンドウでは、<xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A>から文字列を取得します。

### <a name="to-specify-localized-help-strings"></a>ローカライズされたヘルプ文字列を指定するには

1. タイプ ライブラリ ( `helpstringdll` ) のライブラリ ステートメントに`typelib`属性を追加します。

   > [!NOTE]
   > この手順は、タイプ ライブラリがオブジェクト ライブラリ (.olb) ファイルにある場合は省略可能です。

2. 文字列の `helpstringcontext` 属性を指定します。 `helpstring` 属性を指定することもできます。

    これらの属性は、実際の.chm ファイルのヘルプ トピックに含まれる `helpfile` 属性と `helpcontext` 属性とは異なります。

   強調表示されたプロパティ名に表示される説明情報を取得するには、[**プロパティ]** ウィンドウで、<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A>選択したプロパティを呼び出して、出力文字列`lcid`に必要な属性を指定します。 内部的には、<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> は `helpstringdll` 属性で指定された .dll ファイルを検索し、指定されたコンテキストと `lcid` 属性を使ってその .dll ファイル上に `DLLGetDocumentation` を呼び出します。

   `DLLGetDocumentation` の署名と実装は次のとおりです。

```cpp
STDAPI DLLGetDocumentation
(
   ITypeLib * /* ptlib */,
   ITypeInfo * /* ptinfo */,
   LCID /* lcid */,
   DWORD dwCtx,
   BSTR * pbstrHelpString
);
```

 `DLLGetDocumentation` 関数はDLL の .def ファイルで定義されているエクスポートである必要があります。

 内部的には、実際には DLL である .olb ファイルが作成されます。 この DLL には、1 つのリソース、タイプ ライブラリ (.tlb) ファイル、および 1 つのエクスポートされた `DLLGetDocumentation`関数が含まれます。

 .olb ファイルの場合は、 `helpstringdll` 属性は.tlb ファイル自体を含む同じファイルであるため省略可能です。

 したがって、 **[説明]** ウィンドウに表示する文字列を取得するために最低限必要な操作は、タイプ ライブラリに `helpstring` 属性を指定することです。 これらの文字列をローカライズする場合は、 `helpstringdll` (省略可能) 属性と `helpstringcontext` (必須) 属性を指定し、 `DLLGetDocumentation`を実装する必要があります

 idl の `helpstringcontext` 属性と `DLLGetDocumentation`によって取得したローカライズされた情報を取得する場合は、実装する必要のある追加のインターフェイスはありません。

 別の方法でプロパティのローカライズされた名前と説明の取得には、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A> を実装します。 このメソッドの実装に関する詳細については、「 [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
