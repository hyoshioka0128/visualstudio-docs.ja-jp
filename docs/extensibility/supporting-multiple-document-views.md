---
title: 複数のドキュメント ビューをサポートする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - multiple document views
ms.assetid: c7ec2366-91c4-477f-908d-e89068bdb3e3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a952414fa7156d80675564e519e556ccedd524a3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699549"
---
# <a name="supporting-multiple-document-views"></a>複数のドキュメント ビューのサポート
エディター用に別のドキュメント データとドキュメント ビュー オブジェクトを作成することで、ドキュメントの複数のビューを提供できます。 追加のドキュメント ビューが役立つ場合は、次のようになります。

- 新しいウィンドウのサポート: エディターでウィンドウを開いているユーザーがウィンドウ**メニューから****新しい**ウィンドウを開くことができるように、同じ種類のビューを 2 つ以上提供する必要があります。

- フォームとコード ビューのサポート: エディターでさまざまな種類のビューを提供する必要があります。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]たとえば、フォーム ビューとコード ビューの両方を提供します。

  詳細については、Visual Studio パッケージ テンプレートによって作成されたカスタム エディター プロジェクトのEditorFactory.cs ファイルの CreateEditorInstance プロシージャを参照してください。 このプロジェクトの詳細については、「チュートリアル[: カスタム エディターの作成](../extensibility/walkthrough-creating-a-custom-editor.md)」を参照してください。

## <a name="synchronizing-views"></a>ビューの同期
 複数のビューを実装する場合、ドキュメント データ オブジェクトは、すべてのビューをデータと同期させる役割を担います。 イベント処理インターフェイスを使用<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>して、複数のビューをデータと同期できます。

 オブジェクトを使用して複数の<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>ビューを同期しない場合は、ドキュメント データ オブジェクトに加えられた変更を処理する独自のイベント システムを実装する必要があります。 さまざまなレベルの詳細を使用して、複数のビューを最新の状態に保つことができます。 最大粒度の設定を使用すると、1 つのビューに入力すると、他のビューが直ちに更新されます。 最小の粒度では、他のビューはアクティブ化されるまで更新されません。

## <a name="determining-whether-document-data-is-already-open"></a>ドキュメント データが既に開かれているかどうかを確認する
 次の図に示すように、統合開発環境 (IDE) で実行中のドキュメント テーブル (RDT) を使用して、ドキュメントのデータが既に開いているかどうかを追跡できます。

 ![グラフィックを表示します](../extensibility/media/docdataview.gif "ドクデータビュー")。複数のビュー

 既定では、各ビュー (ドキュメント ビュー オブジェクト) は、独自の<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>ウィンドウ フレーム ( ) に含まれています。 ただし、既に説明したように、ドキュメント データは複数のビューで表示できます。 これを有効にするために、Visual Studio は RDT をチェックして、問題のドキュメントが既にエディターで開かれているかどうかを確認します。 IDE がエディター<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>を作成するために呼び出すと、`punkDocDataExisting`パラメーターに NULL 以外の値が返されると、ドキュメントが別のエディターで既に開かれ、そのドキュメントが開かなければならないことを示します。 RDT の機能の詳細については、「[ドキュメント テーブルの実行](../extensibility/internals/running-document-table.md)」を参照してください。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>実装で返されたドキュメント データ オブジェクト`punkDocDataExisting`を調べて、ドキュメント データがエディターに適しているかどうかを判断します。 (たとえば、HTML エディターで表示されるのは HTML データだけです。適切な場合は、エディター ファクトリにデータの 2 番目のビューを提供する必要があります。 このパラメータ`punkDocDataExisting`が`NULL`、別のエディタでドキュメント データ オブジェクトを開いているか、または同じエディタでドキュメント データが既に別のビューで開かれている可能性があります。 ドキュメント データが、エディター ファクトリでサポートされていない別のエディターで開かれている場合、Visual Studio はエディター ファクトリを開くに失敗します。 詳細については、「[方法 : ドキュメント データにビューを添付する](../extensibility/how-to-attach-views-to-document-data.md)」を参照してください。
