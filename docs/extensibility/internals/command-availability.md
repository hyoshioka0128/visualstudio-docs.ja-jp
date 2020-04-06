---
title: コマンドの可用性 |マイクロソフトドキュメント
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dca47d9ed9968c101e3b6b859b51c1cd8d7404db
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709698"
---
# <a name="command-availability"></a>コマンドの可用性

Visual Studio コンテキストは、使用できるコマンドを決定します。 コンテキストは、現在のプロジェクト、現在のエディター、読み込まれる VSPackage、および統合開発環境 (IDE) のその他の側面によって異なります。

## <a name="command-contexts"></a>コマンド コンテキスト

最も一般的なコマンド コンテキストは次のとおりです。

- IDE: IDE によって提供されるコマンドは、常に使用可能です。

- VSPackage: VSPackage は、コマンドを表示または非表示にするタイミングを定義できます。

- プロジェクト: プロジェクトコマンドは、現在選択されているプロジェクトに対してのみ表示されます。

- 編集者:一度にアクティブにできるエディタは1つだけです。 アクティブなエディターからのコマンドを使用できます。 エディターは、言語サービスと密接に連携します。 言語サービスは、関連付けられたエディターのコンテキストでコマンドを処理する必要があります。

- ファイルの種類: エディターは、複数の種類のファイルを読み込むことができます。 使用可能なコマンドは、ファイルの種類によって異なります。

- アクティブ ウィンドウ: 最後のアクティブなドキュメント ウィンドウは、キー バインドのユーザー インターフェイス (UI) コンテキストを設定します。 ただし、内部 Web ブラウザーに似たキー バインド テーブルを持つツール ウィンドウも、UI コンテキストを設定できます。 HTML エディターなどの複数タブのドキュメント ウィンドウでは、各タブは異なるコマンド コンテキスト GUID を持ちます。 ツール ウィンドウを登録すると、常に **[表示]** メニューから使用できるようになります。

- UI コンテキスト: UI コンテキストは、たとえば、ソリューション<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT>がビルドされるとき、または<xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid><xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>デバッガーがアクティブな場合など、クラスの値によって識別されます。 複数の UI コンテキストを同時にアクティブにできます。

## <a name="define-custom-context-guids"></a>カスタム コンテキスト GUID の定義

適切なコマンド コンテキスト GUID が定義されていない場合は、VSPackage で定義し、コマンドの可視性を制御するために必要に応じてアクティブまたは非アクティブにプログラムできます。

1. メソッドを呼び出してコンテキスト<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>GUID を登録します。

2. メソッドを呼び出してコンテキスト GUID<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>の状態を取得します。

3. メソッドを呼び出してコンテキスト GUID の<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>オン/オフを切り上げる。

> [!CAUTION]
> 他の VSPackage が依存する可能性があるため、VSPackage が既存のコンテキスト GUID に影響を与えないことを確認します。

## <a name="see-also"></a>関連項目

- [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
