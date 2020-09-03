---
title: プロパティを表示する Grid |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5fd5e17d764336cda450c726023b209f89f194a1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180393"
---
# <a name="properties-display-grid"></a>プロパティ表示グリッド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[ **プロパティ** ] ウィンドウには、グリッド内のフィールドが表示されます。 左側の列には、プロパティ名が含まれています。右側の列には、プロパティ値が含まれています。  
  
## <a name="working-with-the-grid"></a>グリッドの操作  
 2列の一覧には、構成に依存しないプロパティが表示されます。これらのプロパティは、デザイン時およびその現在の設定で変更できます。 すべてのプロパティが表示されない場合があることに注意してください。 たとえば、メソッドを実装することによって、プロパティを非表示に設定でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> ます。 具体的には、子プロパティを持つプロパティを非表示にするには、子プロパティを [持つ](../../misc/hiding-properties-that-have-child-properties.md)プロパティを非表示にします。  
  
 情報を **プロパティ** ウィンドウにプッシュするには、IDE でを使用 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> します。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、[ **プロパティ** ] ウィンドウに表示される、関連するプロパティを持つ選択可能なオブジェクトを含むウィンドウごとに、vspackage によって呼び出されます。 **ソリューションエクスプローラー**の呼び出しの実装は、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> `GetProperty` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> プロジェクト階層内でを使用して、階層内のすべてのオブジェクトを取得します。  
  
 VSPackage でがサポートされていない場合 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 、IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 階層項目または項目が提供する値を使用してを使用しようとします。  
  
 プロジェクト VSPackage を作成する必要はありません <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 。これは、それを実装する IDE 提供のウィンドウパッケージ ( **ソリューションエクスプローラー**など) がその代わりに構築されるため <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> です。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> は、IDE によって呼び出される3つのメソッドで構成されます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> [ **プロパティ** ] ウィンドウに表示されるように選択されたオブジェクトの数を格納します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A>`IDispatch`[**プロパティ**] ウィンドウに表示されるように選択されたオブジェクトを返します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> によって返されるオブジェクトを <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> ユーザーが選択できるようにします。 これにより、UI でユーザーに表示される選択内容を VSPackage が視覚的に更新できるようになります。  
  
  [ **プロパティ** ] ウィンドウは、 `IDispatch` 参照されるプロパティを取得するために、オブジェクトから情報を抽出します。 プロパティブラウザーは、を使用して、で `IDispatch` サポートされているプロパティを照会し `ITypeInfo` ます。これは、から取得 `IDispatch::GetTypeInfo` します。 次に、ブラウザーはこれらの値を使用して、[ **プロパティ** ] ウィンドウを設定し、グリッドに表示される個々のプロパティの値を変更します。 プロパティ情報は、オブジェクト内で保持されます。  
  
  返されたオブジェクトはをサポートするため `IDispatch` 、呼び出し元はまたはを呼び出して、 `IDispatch::Invoke` 必要な `ITypeInfo::Invoke` 情報を表す定義済みのディスパッチ識別子 (DISPID) を指定して、オブジェクトの名前などの情報を取得できます。 Dispid は、ユーザー定義の識別子と競合しないようにするために負の値です。  
  
  [ **プロパティ** ] ウィンドウには、選択したオブジェクトの特定のプロパティの属性に応じて、さまざまな種類のフィールドが表示されます。 これらのフィールドには、エディットボックス、ドロップダウンリスト、およびカスタムエディターダイアログボックスへのリンクが含まれます。  
  
- 列挙されたリストに含まれる値は、クエリによってに取得され <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> `IDispatch` ます。 列挙された一覧から取得した値は、[プロパティ] グリッドで、フィールド名をダブルクリックするか、値をクリックしてドロップダウンリストから新しい値を選択することによって変更できます。 列挙されたリストの設定が定義されているプロパティの場合、[プロパティ] の一覧でプロパティ名をダブルクリックすると、使用可能な選択肢が順番に表示されます。 True/false などの2つの選択肢だけを持つ定義済みプロパティの場合は、プロパティ名をダブルクリックして選択範囲を切り替えます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A>が `false` で、値が変更されたことを示している場合、値は太字で表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> は、値を元の値にリセットできるかどうかを判断するために使用されます。 その場合は、値を右クリックし、表示されるメニューから [ **リセット** ] を選択して、既定値に戻すことができます。 それ以外の場合は、値を既定値に戻して手動で変更する必要があります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> では、デザイン時に表示されるプロパティの名前をローカライズおよび非表示にすることもできますが、実行時に表示されるプロパティ名には影響しません。  
  
- 省略記号ボタン ([...]) をクリックすると、ユーザーが選択できるプロパティ値の一覧が表示されます (カラーピッカーやフォント一覧など)。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> これらの値を提供します。  
  
## <a name="see-also"></a>参照  
 [プロパティの拡張](../../extensibility/internals/extending-properties.md)
