---
title: プロパティウィンドウのフィールドとインターフェイス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b58314d64536ecf33cc5589609ee5524a9352629
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700822"
---
# <a name="properties-window-fields-and-interfaces"></a>プロパティ ウィンドウのフィールドとインターフェイス
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[ **プロパティ** ] ウィンドウに表示される情報を決定するために選択するモデルは、IDE にフォーカスがあるウィンドウに基づいています。 すべてのウィンドウおよび選択したウィンドウ内のオブジェクトは、選択コンテキストオブジェクトをグローバル選択コンテキストにプッシュできます。 環境では、ウィンドウにフォーカスがあるときに、ウィンドウフレームの値を使用してグローバル選択コンテキストを更新します。 フォーカスが変更されると、選択コンテキストが変わります。  
  
## <a name="tracking-selection-in-the-ide"></a>IDE での選択の追跡  
 IDE によって所有されているウィンドウフレームまたはサイトには、という名前のサービスがあり <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ます。 次の手順では、[**プロパティ**] ウィンドウに表示される内容を変更するために、ユーザーが別の開いているウィンドウにフォーカスを変更したり、**ソリューションエクスプローラー**で別のプロジェクト項目を選択したりすることによって発生する、選択項目の変更について説明します。  
  
1. 選択したウィンドウに配置されている VSPackage によって作成されたオブジェクトは、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> を呼び出すためにを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> ます。  
  
2. 選択したウィンドウによって提供される選択コンテナーによって、独自のオブジェクトが作成され <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。 選択が変更されると、VSPackage はを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 変更の **プロパティ** ウィンドウを含む、環境内のリスナーに通知します。 また、新しい選択に関連する階層と項目情報へのアクセスも提供されます。  
  
3. <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>を呼び出し、パラメーターに選択した階層項目を渡すと、オブジェクトが設定され `VSHPROPID_BrowseObject` <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。  
  
4. 要求された項目に対して [IDispatch インターフェイス](https://msdn.microsoft.com/ebbff4bc-36b2-4861-9efa-ffa45e013eb5) から派生したオブジェクトが返され、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 環境がそれをにラップし <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます (次の手順を参照)。 呼び出しが失敗した場合、環境はへの2回目の呼び出しを行い `IVsHierarchy::GetProperty` 、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 階層項目または項目が提供する選択コンテナーを渡します。  
  
    プロジェクト VSPackage は、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> それを実装する環境指定のウィンドウ VSPackage ( **ソリューションエクスプローラー**など) が <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> その代わりに構築されるため、作成されません。  
  
5. 環境では、のメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> インターフェイスに基づいてオブジェクトを取得し、[ `IDispatch` **プロパティ** ] ウィンドウに入力します。  
  
   [ **プロパティ** ] ウィンドウの値が変更された場合、vspackage は `IVsTrackSelectionEx::OnElementValueChangeEx` を実装し、 `IVsTrackSelectionEx::OnSelectionChangeEx` 要素の値に変更を報告します。 次に、またはを呼び出して、[ <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> **プロパティ** ] ウィンドウに表示されている情報をプロパティ値と同期させます。 詳細については、「 [プロパティウィンドウでのプロパティ値の更新](../../misc/updating-property-values-in-the-properties-window.md)」を参照してください。  
  
   **ソリューションエクスプローラー**で別のプロジェクトアイテムを選択してそのアイテムに関連するプロパティを表示することに加えて、[**プロパティ**] ウィンドウのドロップダウンリストを使用して、フォームまたはドキュメントウィンドウ内から別のオブジェクトを選択することもできます。 詳細については、「[ [プロパティ] ウィンドウオブジェクトリスト](../../extensibility/internals/properties-window-object-list.md)」を参照してください。  
  
   [ **プロパティ** ] ウィンドウのグリッドでの情報の表示方法をアルファベット順からカテゴリ別に変更できます。また、使用可能な場合は、[ **プロパティ** ] ウィンドウの該当するボタンをクリックして、選択したオブジェクトのプロパティページを開くこともできます。 詳細については、「 [プロパティウィンドウのボタン](../../extensibility/internals/properties-window-buttons.md) と [プロパティページ](../../extensibility/internals/property-pages.md)」を参照してください。  
  
   最後に、 **[プロパティ]** ウィンドウの下部には、[ **プロパティ** ] ウィンドウのグリッドで選択したフィールドの説明も表示されます。 詳細については、「 [プロパティウィンドウからのフィールドの説明の取得](../../misc/getting-field-descriptions-from-the-properties-window.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [プロパティの拡張](../../extensibility/internals/extending-properties.md)
