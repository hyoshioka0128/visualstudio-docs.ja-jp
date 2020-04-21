---
title: 'チュートリアル: カスタム エディターに機能を追加する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65ef0edf76780ba7c8b6f5d9347195c286bec466
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649843"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>チュートリアル: カスタム エディターに機能を追加する
カスタム エディターを作成した後、そのエディターに機能を追加できます。

## <a name="to-create-an-editor-for-a-vspackage"></a>VS パッケージのエディターを作成するには

1. Visual Studio パッケージ プロジェクト テンプレートを使用してカスタム エディターを作成します。

     詳細については、「[チュートリアル: カスタム エディターの作成」を](../extensibility/walkthrough-creating-a-custom-editor.md)参照してください。

2. エディターで 1 つのビューをサポートするか、複数のビューをサポートするかを決定します。

     **[新しいウィンドウ]** コマンドをサポートするエディタ、またはフォーム ビューとコード ビューを備えたエディターには、個別のドキュメント データ オブジェクトとドキュメント ビュー オブジェクトが必要です。 1 つのビューのみをサポートするエディターでは、ドキュメント データ オブジェクトとドキュメント ビュー オブジェクトを同じオブジェクトに実装できます。

     複数のビューの例については、[複数のドキュメント ビューをサポートする](../extensibility/supporting-multiple-document-views.md)を参照してください。

3. インターフェイスを設定して、エディター ファクトリ<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>を実装します。

     詳細については、「[ファクトリのエディタ](/visualstudio/extensibility/editor-factories?view=vs-2015)」を参照してください。

4. ドキュメント ビュー オブジェクト ウィンドウを管理するために、エディターで埋め込み先編集を行うか、埋め込みを簡略化するかを決定します。

     簡易埋め込みエディター ウィンドウは標準のドキュメント ビューをホストし、埋め込みアクティブ化エディター ウィンドウは ActiveX コントロールまたはその他のアクティブ オブジェクトをドキュメント ビューとしてホストします。 詳細については、「[簡易埋め込み](../extensibility/simplified-embedding.md)と[埋め込み場所でのアクティブ化](/visualstudio/misc/in-place-activation?view=vs-2015)」を参照してください。

5. コマンドを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>処理するインターフェイスを実装します。

6. 外部ファイルの変更に対するドキュメントの永続性と応答を提供します。

    1. ファイルを永続化するには、エディター<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>の<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>ドキュメント データ オブジェクトを実装し、その上に置いてください。

    2. 外部ファイルの変更に応答するには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx>エディタ<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>のドキュメント データ オブジェクトを実装し、そのオブジェクトに対して実行します。

        > [!NOTE]
        > を`QueryService`指<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>すポインタを取得するために`IVsFileChangeEx`呼び出します。

7. ドキュメント編集イベントをソース コード管理に関連付けます。 次の手順に従います。

    1. で呼び出`IVsQueryEditQuerySave2``QueryService`すことによって、ポインタ<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>を取得します。

    2. 最初の編集イベントが発生したら、メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>呼び出します。

         このメソッドは、ファイルがまだチェックアウトされていない場合は、ユーザーにチェックアウトを求めるプロンプトを表示します。エラーを回避するためには、必ず "チェックアウトされていないファイル" 条件を処理してください。

    3. 同様に、ファイルを保存する前に<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>、メソッドを呼び出します。

         このメソッドは、ファイルが保存されていない場合、または最後の保存以降に変更された場合に、ファイルを保存するように求めるメッセージを表示します。

8. **[プロパティ]** ウィンドウを有効にすると、エディターで選択したテキストのプロパティが表示されます。 次の手順に従います。

    1. の<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>実装を渡して、テキストの選択が変更されるたびに<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>呼び出します。

    2. サービス`QueryService`を<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>呼び出して、<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>へのポインターを取得します。

9. ユーザーが、エディターと**ツールボックス**の間、または外部のエディター (Microsoft Word など) とツールボックス の間で項目をドラッグ アンド ドロップ**できるようにします**。 次の手順に従います。

    1. エディター`IDropTarget`がドロップターゲットであることを IDE に通知するために、エディターを実装します。

    2. エディターが<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>**ツールボックス**の項目を有効または無効にできるように、ビューにインターフェイスを実装します。

    3. を<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A>実装し`QueryService`、<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox>および<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>インターフェイスへのポインターを取得<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>するサービスを呼び出します。

         これらの手順を使用すると、VSPackage は新しい項目をツールボックスに追加**できます**。

10. エディターに他のオプション機能を使用するかどうかを決定します。

    - エディターで検索コマンドと置換コマンドをサポートする場合は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>を実装します。

    - エディターでドキュメント アウトライン ツール ウィンドウを使用する場合は、`IVsDocOutlineProvider`を実装します。

    - エディターでステータス バーを使用する場合は、 を<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>実装し`QueryService`、<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>へのポインターを取得`IVsStatusBar`する を呼び出します。

         たとえば、エディターは、行/列情報、選択モード(ストリーム/ボックス)、挿入モード(挿入/オーバーストライク)を表示することができます。

    - エディターで`Undo`コマンドをサポートする場合は、OLE 元に戻すマネージャー モデルを使用することをお勧めします。 代わりに、エディタに直接コマンドを`Undo`処理させることができます。

11. VSPackage、メニュー、エディター、およびその他の機能の GUID を含む、レジストリ情報を作成します。

     エディターを適切に登録する方法を示すために *.rgs*ファイル スクリプトに記述するコードの一般的な例を次に示します。

    ```csharp
    NoRemove Editors
    {
          ForceRemove {...guidEditor...} = s 'RTF Editor'
          {
             val Package = s '{...guidVsPackage...}'
             ForceRemove Extensions
             {
                val rtf = d 50
             }
          }
    }
    NoRemove Menus
    {
          val {...guidVsPackage...} = s ',203,11'
    }
    ```

12. 状況依存のヘルプ サポートを実装する。

     この手順では、エディターの項目に対して F1 ヘルプとダイナミック ヘルプ ウィンドウのサポートを提供できます。 詳細については、「[方法 : エディターのコンテキストを提供する](/visualstudio/extensibility/how-to-provide-context-for-editors?view=vs-2015)」を参照してください。

13. インターフェイスを実装して、エディターからオートメーション オブジェクト`IDispatch`モデルを公開します。

     詳細については、「 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)」を参照してください。

## <a name="robust-programming"></a>信頼性の高いプログラミング

- エディターインスタンスは、IDE がメソッドを呼<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>び出すと作成されます。 エディターが複数のビューをサポート`CreateEditorInstance`している場合は、ドキュメント データとドキュメント ビュー オブジェクトの両方を作成します。 ドキュメント データ オブジェクトが既に開いている場合は、NULL 以外`punkDocDataExisting`の`IVsEditorFactory::CreateEditorInstance`値が に渡されます。 エディター ファクトリの実装では、既存のドキュメント データ オブジェクトに対して適切なインターフェイスを照会することによって、互換性があるかどうかを判断する必要があります。 詳細については、「[複数のドキュメント ビューをサポートする](../extensibility/supporting-multiple-document-views.md)」を参照してください。

- 簡略化された埋め込み方法を使用する場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>インターフェイスを実装します。

- インプレース アクティベーションを使用する場合は、次のインターフェイスを実装します。

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > インターフェイス`IOleInPlaceComponent`は、OLE 2 メニューのマージを回避するために使用されます。

   実装`IOleCommandTarget`では、**切り取り**、**コピー**、**貼り付け**などのコマンドを処理します。 を実装`IOleCommandTarget`する際に、エディターで独自のコマンド メニュー構造を定義するために独自の *.vsct*ファイルが必要かどうか、または[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]によって定義された標準コマンドを実装できるかどうかを決定します。 通常、エディタは IDE のメニューを使用および拡張し、独自のツールバーを定義します。 ただし、エディタは、IDE の標準コマンドセットを使用するだけでなく、独自のコマンドを定義する必要があります。 エディターは、使用する標準コマンドを宣言し、新しいコマンド、コンテキスト メニュー、トップレベル メニュー、および *.vsct*ファイル内のツール バーを定義する必要があります。 インプレース アクティブ化エディターを作成する場合<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>は、OLE 2 メニューのマージを使用する代わりに *、.vsct*ファイルでエディターのメニューとツール バーを実装および定義します。

- UI でメニュー コマンドが混雑しないようにするには、新しいコマンドを作成する前に、IDE の既存のコマンドを使用する必要があります。 共有コマンドは、*次の中*で定義*されています。* これらのファイルは、既定でインストールの VisualStudioIntegration\Common\Inc サブディレクトリに[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]インストールされます。

- `ISelectionContainer`単一選択と複数選択の両方を表すことができます。 選択された各オブジェクトは、`IDispatch`オブジェクトとして実装されます。

- IDE は、`IOleUndoManager`を<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>介して<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>インスタンス化できる オブジェクトまたは からアクセスできるサービスとして実装します。 エディターは、各`IOleUndoUnit``Undo`アクションのインターフェイスを実装します。

- カスタム エディターでオートメーション オブジェクトを公開できる場所は 2 つあります。

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>関連項目

- [オートメーションモデルへの貢献](../extensibility/internals/contributing-to-the-automation-model.md)
