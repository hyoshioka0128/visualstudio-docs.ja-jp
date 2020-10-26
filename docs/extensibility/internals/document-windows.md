---
title: ドキュメントウィンドウ |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 38556eec259e91dd9e007d8e9bf1ac8d59f159a0
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90011763"
---
# <a name="document-windows"></a>ドキュメント ウィンドウ
Visual Studio では、 *ドキュメントウィンドウ* は、マルチドキュメントインターフェイス (MDI) ウィンドウに関連付けられている、フレーム化された子ウィンドウです。 通常、ドキュメントウィンドウは、ソースコードまたはテキストの表示と変更に使用されますが、他の機能型をホストすることもできます。 ドキュメントウィンドウ:

- は、複数のファイルを同時に表示できるように、親 MDI の個別の水平または垂直タブグループに整理できます。

- 親 MDI の任意の順序でドッキングできます。

- 自由にフローティングできます。

- タブオーダーで他の MDI ウィンドウにリンクされています。

  グループ化、ドッキング、フローティングのコマンドは、[ドキュメントウィンドウ] タブのショートカットメニューにあります。

  Visual Studio でのウィンドウの動作の詳細については、「 [ウィンドウレイアウトをカスタマイズ](../../ide/customizing-window-layouts-in-visual-studio.md)する」を参照してください。

## <a name="document-window-implementation"></a>ドキュメントウィンドウの実装
 ドキュメントウィンドウは、エディターを実装することによって作成されます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> エディターのインスタンス化の一部としてドキュメントウィンドウを作成します。 詳細については、「 [従来のインターフェイス](../../vs-2015/extensibility/legacy-interfaces-in-the-editor.md?view=vs-2015)」を参照してください。

> [!NOTE]
> ウィンドウに移動ナビゲーションポイントを提供するには、インターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> ます。 テキストエディターでは、ドキュメント内のナビゲーションポイントを識別するためにテキストマーカーが使用されます。

## <a name="the-running-document-table"></a>実行中のドキュメントテーブル
 IDE は、実行中のドキュメントテーブル (RDT) を使用して、すべてのドキュメントウィンドウの状態を追跡します。 RDT は、ドキュメントウィンドウにイベントが通知されるメカニズムです。たとえば、ソリューションが閉じられた場合や、ファイルが編集された場合などです。 詳細については、「 [document table の実行](../../extensibility/internals/running-document-table.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ドキュメントの読み込みの遅延](../../extensibility/internals/delayed-document-loading.md)