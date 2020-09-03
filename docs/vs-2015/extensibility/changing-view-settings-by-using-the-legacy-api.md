---
title: 従来の API を使用して表示設定を変更する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - changing view settings
ms.assetid: 12c9b300-0894-4124-96a1-764326176d77
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7d58d1477b9d7f58242f8cb4db7c3c360c248b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184464"
---
# <a name="changing-view-settings-by-using-the-legacy-api"></a>レガシ API を使用する表示設定の変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザーは、[ **オプション** ] ダイアログボックスを使用して、[右端での折り返し]、[選択範囲の余白]、[仮想空間] などの主要なエディター機能の設定を変更できます。 ただし、これらの設定はプログラムによって変更することもできます。  
  
## <a name="changing-settings-by-using-the-legacy-api"></a>レガシ API を使用した設定の変更  
 インターフェイスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> テキストエディターの一連のプロパティを公開します。 テキストビューには、プログラムによってテキストビューの設定が変更されたグループを表すプロパティ (GUID_EditPropCategory_View_MasterSettings) のカテゴリが含まれています。 この方法で表示設定を変更すると、リセットされるまで [ **オプション** ] ダイアログボックスで変更することはできません。  
  
 コアエディターのインスタンスのビュー設定を変更する一般的な手順を次に示します。  
  
1. `QueryInterface` <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> インターフェイスの () でを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> ます。  
  
2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A>パラメーターに GUID_EditPropCategory_View_MasterSettings の値を指定して、メソッドを呼び出し `rguidCategory` ます。  
  
     この操作を行うと、インターフェイスへのポインターが返されます。このインターフェイスには、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> ビューの強制プロパティのセットが含まれています。 このグループの設定は完全に強制されます。 このグループに設定されていない設定は、[ **オプション** ] ダイアログボックスまたはユーザーのコマンドで指定されたオプションに従って実行されます。  
  
3. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A>パラメーターに適切な設定値を指定して、メソッドを呼び出し `idprop` ます。  
  
     たとえば、ワードラップを強制的に実行するには、を呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> パラメーターに VSEDITPROPID_ViewLangOpt_WordWrap の値を指定し `vt` `idprop` ます。 この呼び出しで、 `vt` は VT_BOOL 型のバリアントで、 `vt.boolVal` は VARIANT_TRUE です。  
  
## <a name="resetting-changed-view-settings"></a>変更されたビュー設定のリセット  
 コアエディターのインスタンスに対して変更されたビュー設定をリセットするには、メソッドを呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> パラメーターに適切な設定値を指定し `idprop` ます。  
  
 たとえば、単語の折り返しを自由にフローティングできるようにするには、を呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.RemoveProperty%2A> パラメーターに VSEDITPROPID_ViewLangOpt_WordWrap の値を指定して、プロパティカテゴリからそれを削除し `idprop` ます。  
  
 コアエディターに対して変更された設定をすべて一度に削除するには、パラメーターに VSEDITPROPID_ViewComposite_AllCodeWindowDefaults、vt の値を指定し `idprop` ます。 この呼び出しでは、vt は VT_BOOL 型のバリアントで、vt は VARIANT_TRUE です。  
  
## <a name="see-also"></a>参照  
 [コアエディター内](../extensibility/inside-the-core-editor.md)   
 [レガシ API を使用したテキストビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)   
 [[オプション] ダイアログボックス](../ide/reference/options-dialog-box-visual-studio.md)
