---
title: ドキュメントウィンドウ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5e62be456422b7ee5e9f2828a44a6be05e1211d9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841528"
---
# <a name="document-windows"></a>ドキュメント ウィンドウ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio では、 *ドキュメントウィンドウ* は、マルチドキュメントインターフェイス (MDI) ウィンドウに関連付けられている、フレーム化された子ウィンドウです。 通常、ドキュメントウィンドウは、ソースコードまたはテキストの表示と変更に使用されますが、他の機能型をホストすることもできます。 ドキュメントウィンドウ:  
  
- は、複数のファイルを同時に表示できるように、親 MDI の個別の水平または垂直タブグループに整理できます。  
  
- 親 MDI の任意の順序でドッキングできます。  
  
- 自由にフローティングできます。  
  
- タブオーダーで他の MDI ウィンドウにリンクされています。  
  
  グループ化、ドッキング、フローティングのコマンドは、[ドキュメントウィンドウ] タブのショートカットメニューにあります。  
  
  Visual Studio でのウィンドウの動作の詳細については、「 [ウィンドウレイアウトをカスタマイズ](../../ide/customizing-window-layouts-in-visual-studio.md)する」を参照してください。  
  
## <a name="document-window-implementation"></a>ドキュメントウィンドウの実装  
 ドキュメントウィンドウは、エディターを実装することによって作成されます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> エディターのインスタンス化の一部としてドキュメントウィンドウを作成します。 詳細については、「 [従来のインターフェイス](../../extensibility/legacy-interfaces-in-the-editor.md)」を参照してください。  
  
> [!NOTE]
> ウィンドウに移動ナビゲーションポイントを提供するには、インターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> ます。 テキストエディターでは、ドキュメント内のナビゲーションポイントを識別するためにテキストマーカーが使用されます。  
  
## <a name="the-running-document-table"></a>実行中のドキュメントテーブル  
 IDE は、実行中のドキュメントテーブル (RDT) を使用して、すべてのドキュメントウィンドウの状態を追跡します。 RDT は、ドキュメントウィンドウにイベントが通知されるメカニズムです。たとえば、ソリューションが閉じられた場合や、ファイルが編集された場合などです。 詳細については、「 [Document Table の実行](../../extensibility/internals/running-document-table.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ドキュメントの読み込みの遅延](../../extensibility/internals/delayed-document-loading.md)
