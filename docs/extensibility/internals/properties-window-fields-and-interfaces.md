---
title: プロパティウィンドウのフィールドとインターフェイス |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706159"
---
# <a name="properties-window-fields-and-interfaces"></a>プロパティ ウィンドウのフィールドとインターフェイス
[ **プロパティ** ] ウィンドウに表示される情報を決定するために選択するモデルは、IDE にフォーカスがあるウィンドウに基づいています。 すべてのウィンドウおよび選択したウィンドウ内のオブジェクトは、選択コンテキストオブジェクトをグローバル選択コンテキストにプッシュできます。 環境では、ウィンドウにフォーカスがあるときに、ウィンドウフレームの値を使用してグローバル選択コンテキストを更新します。 フォーカスが変更されると、選択コンテキストが変わります。

## <a name="tracking-selection-in-the-ide"></a>IDE での選択の追跡
 IDE によって所有されているウィンドウフレームまたはサイトには、という名前のサービスがあり <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ます。 次の手順では、[**プロパティ**] ウィンドウに表示される内容を変更するために、ユーザーが別の開いているウィンドウにフォーカスを変更したり、**ソリューションエクスプローラー**で別のプロジェクト項目を選択したりすることによって発生する、選択項目の変更について説明します。

1. 選択したウィンドウに配置されている VSPackage によって作成されたオブジェクトは、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> を呼び出すためにを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> ます。

2. 選択したウィンドウによって提供される選択コンテナーによって、独自のオブジェクトが作成され <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。 選択が変更されると、VSPackage はを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 変更の **プロパティ** ウィンドウを含む、環境内のリスナーに通知します。 また、新しい選択に関連する階層と項目情報へのアクセスも提供されます。

3. <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>を呼び出し、パラメーターに選択した階層項目を渡すと、オブジェクトが設定され `VSHPROPID_BrowseObject` <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。

4. __VSHPROPID に対して、 [IDispatch インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) から派生したオブジェクトが返され [ます。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) 要求された項目の VSHPROPID_BrowseObject し、環境がそれをにラップし <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます (次の手順を参照)。 呼び出しが失敗した場合、環境はの2回目の呼び出しを行い `IVsHierarchy::GetProperty` 、選択コンテナー __VSHPROPID を渡し [ます。](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) 階層項目が提供する VSHPROPID_SelContainer ます。

    プロジェクト VSPackage は、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> それを実装する環境指定のウィンドウ VSPackage ( **ソリューションエクスプローラー**など) が <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> その代わりに構築されるため、作成されません。

5. 環境では、のメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> インターフェイスに基づいてオブジェクトを取得し、[ `IDispatch` **プロパティ** ] ウィンドウに入力します。

   [ **プロパティ** ] ウィンドウの値が変更された場合、vspackage は `IVsTrackSelectionEx::OnElementValueChangeEx` を実装し、 `IVsTrackSelectionEx::OnSelectionChangeEx` 要素の値に変更を報告します。 次に、またはを呼び出して、[ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> **プロパティ** ] ウィンドウに表示されている情報をプロパティ値と同期させます。 詳細については、「 [プロパティウィンドウでのプロパティ値の更新](#updating-property-values-in-the-properties-window)」を参照してください。

   **ソリューションエクスプローラー**で別のプロジェクトアイテムを選択してそのアイテムに関連するプロパティを表示することに加えて、[**プロパティ**] ウィンドウのドロップダウンリストを使用して、フォームまたはドキュメントウィンドウ内から別のオブジェクトを選択することもできます。 詳細については、「[ [プロパティ] ウィンドウオブジェクトリスト](../../extensibility/internals/properties-window-object-list.md)」を参照してください。

   [ **プロパティ** ] ウィンドウのグリッドでの情報の表示方法をアルファベット順からカテゴリ別に変更できます。また、使用可能な場合は、[ **プロパティ** ] ウィンドウの該当するボタンをクリックして、選択したオブジェクトのプロパティページを開くこともできます。 詳細については、「 [プロパティウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md) と [プロパティページ](../../extensibility/internals/property-pages.md)」を参照してください。

   最後に、 **[プロパティ]** ウィンドウの下部には、[ **プロパティ** ] ウィンドウのグリッドで選択したフィールドの説明も表示されます。 詳細については、「 [プロパティウィンドウからのフィールドの説明の取得](#getting-field-descriptions-from-the-properties-window)」を参照してください。

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a> プロパティウィンドウでのプロパティ値の更新
**[プロパティ]** ウィンドウをプロパティ値の変更と同期するには、2 つの方法があります。 1 番目の方法は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> インターフェイスを呼び出すことです。このインターフェイスは、環境によって用意されているツール ウィンドウやドキュメント ウィンドウのアクセスや作成を含む、基本的なウィンドウ操作機能へのアクセスを提供します。 次の手順は、この同期プロセスを説明したものです。

### <a name="updating-property-values-using-ivsuishell"></a>IVsUIShell を使ってプロパティ値を更新する

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>IVsUIShell インターフェイスを使ってプロパティ値を更新するには

1. VSPackage、プロジェクト、エディターがツール ウィンドウまたはドキュメント ウィンドウを作成したり列挙したりする必要が生じた時点で、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> を (<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> サービスを通じて) 呼び出します。

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A>を実装して、イベントを実装および実行せずに、プロジェクト (または [**プロパティ**] ウィンドウによって参照される他の選択されたオブジェクト) のプロパティの変更とプロパティウィンドウの同期を維持し**Properties** <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> ます。

3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> のメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> を実装します。この 2 つのメソッドは、それぞれ、階層イベントのクライアント通知を設定および無効化します。これにより、階層で <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> を実装する必要がなくなります。

### <a name="updating-property-values-using-iconnection"></a>IConnection を使ってプロパティ値を更新する
 **[プロパティ]** ウィンドウとプロパティ値の変更を同期する 2 番目の方法は、接続可能なオブジェクトに `IConnection` を実装することにより、発信インターフェイスの存在を示すことです。 プロパティ名をローカライズする場合は、オブジェクトを <xref:System.ComponentModel.ICustomTypeDescriptor> から派生させます。 <xref:System.ComponentModel.ICustomTypeDescriptor> の実装では、実装から返すプロパティ記述子を変更し、プロパティの名前を変更できます。 説明をローカライズするには、<xref:System.ComponentModel.DescriptionAttribute> から派生させた属性を作成し、Description プロパティをオーバーライドします。

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>IConnection インターフェイスを実装する際の考慮事項

1. `IConnection` は、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを提供します。 また、すべての接続ポイント サブオブジェクトへのアクセスも提供し、それぞれは <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを実装します。

2. すべての参照オブジェクトは、<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> イベントを実装する必要があります。 **[プロパティ]** ウィンドウは、 `IConnection`を通してイベントを設定することをお勧めします。

3. 接続ポイントは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> の実装で許容される接続数 (1 つまたは複数) を制御します。 インターフェイスを 1 つのみ許容する接続ポイントでは、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> メソッドから <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> を返すことができます。

4. クライアントは、`IConnection` インターフェイスを呼び出すことにより、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを持つ列挙子サブオブジェクトへのアクセスを取得できます。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> インターフェイスを呼び出すと、各発信インターフェイス ID (IID) の接続ポイントを列挙することができます。

5. また、`IConnection` を呼び出すことにより、各発信 IID への <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> インターフェイスを持つ接続ポイント サブオブジェクトへのアクセスを取得することもできます。 クライアントは、インターフェイスを介して、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接続可能オブジェクトとクライアント独自の同期を使用して、アドバイザリループを開始または終了します。クライアントは、インターフェイスを呼び出して、 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> 認識している接続を列挙するためのインターフェイスを持つ列挙子オブジェクトを取得することもできます。

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a> [プロパティ] ウィンドウからのフィールドの説明の取得
**[プロパティ]** ウィンドウの下部にある説明領域に、選択したプロパティ フィールドに関連する情報が表示されます。 この機能は既定で有効になっています。 説明フィールドを非表示にするには、 **[プロパティ]** ウィンドウを右クリックし、 **[説明]** をクリックします。 これにより、メニュー ウィンドウの **[説明]** タイトルの横のチェック マークが削除されます。 同じ手順を行って **[説明]** の表示をオンに戻すことにより、フィールドを再度表示できます。

 説明フィールド内の情報は <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> から取得されます。 それぞれのメソッド、インターフェイス、コクラスなどには、タイプ ライブラリのローカライズされていない `helpstring` 属性を適用できます。 [ **プロパティ** ] ウィンドウで、から文字列を取得し <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> ます。

### <a name="to-specify-localized-help-strings"></a>ローカライズされたヘルプ文字列を指定するには

1. タイプ ライブラリ ( `helpstringdll` ) のライブラリ ステートメントに`typelib`属性を追加します。

   > [!NOTE]
   > この手順は、タイプ ライブラリがオブジェクト ライブラリ (.olb) ファイルにある場合は省略可能です。

2. 文字列の `helpstringcontext` 属性を指定します。 `helpstring` 属性を指定することもできます。

    これらの属性は、実際の.chm ファイルのヘルプ トピックに含まれる `helpfile` 属性と `helpcontext` 属性とは異なります。

   強調表示されているプロパティ名に表示される説明情報を取得するために、[ **プロパティ** ] ウィンドウは、選択されて <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> いるプロパティに対してを呼び出し、出力文字列に必要な属性を指定し `lcid` ます。 内部的には、<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> は `helpstringdll` 属性で指定された .dll ファイルを検索し、指定されたコンテキストと `lcid` 属性を使ってその .dll ファイル上に `DLLGetDocumentation` を呼び出します。

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

## <a name="see-also"></a>こちらもご覧ください

- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
