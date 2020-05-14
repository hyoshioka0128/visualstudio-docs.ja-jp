---
title: ドキュメント ウィンドウ |マイクロソフトドキュメント
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
ms.openlocfilehash: 711033a4ad2e782ecbe509595266426d186bed8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708512"
---
# <a name="document-windows"></a>ドキュメント ウィンドウ
Visual Studio では、*ドキュメント ウィンドウ*は、マルチ ドキュメント インターフェイス (MDI) ウィンドウに関連付けられているフレームの子ウィンドウです。 ドキュメント ウィンドウは、通常、ソース コードやテキストの表示と変更に使用されますが、他の機能型をホストすることもできます。 ドキュメント ウィンドウ:

- 複数のファイルを同時に表示できるように、親 MDI 内の水平タブグループまたは垂直タブ グループを個別に編成できます。

- 親 MDI の任意の順序でドッキングできます。

- 自由に浮かべることができる。

- タブオーダーで他の MDI ウィンドウにリンクされています。

  グループ化、ドッキング、およびフローティングのコマンドは、ドキュメント ウィンドウ タブのショートカット メニューにあります。

  Visual Studio でのウィンドウの動作の詳細については、「[ウィンドウ レイアウトのカスタマイズ](../../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。

## <a name="document-window-implementation"></a>ドキュメント ウィンドウの実装
 ドキュメント ウィンドウは、エディターを実装することによって作成されます。 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>インターフェイスは、エディターのインスタンス化の一部としてドキュメント ウィンドウを作成します。 詳細については、[エディタのレガシーインタフェースを](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)参照してください。

> [!NOTE]
> ウィンドウに前後ナビゲーション ポイントを提供するには、インターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation>します。 テキスト エディタは、テキスト マーカーを使用して、ドキュメント内のナビゲーション ポイントを識別します。

## <a name="the-running-document-table"></a>実行中のドキュメント テーブル
 IDE では、実行中のドキュメントテーブル (RDT) を使用して、すべてのドキュメントウィンドウのステータスを追跡します。 RDT は、ソリューションが閉じられたり、ファイルが編集された場合など、ドキュメント ウィンドウにイベントが通知されるメカニズムです。 詳細については、「ドキュメント[テーブルの実行](../../extensibility/internals/running-document-table.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [遅延ドキュメントの読み込み](../../extensibility/internals/delayed-document-loading.md)
