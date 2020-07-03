---
title: 'チュートリアル: カスタムエディターへの機能の追加 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7605307d24aa320d2f892dc332f9ff78e14114e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905947"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>チュートリアル: カスタムエディターへの機能の追加
カスタムエディターを作成したら、それにさらに機能を追加できます。

## <a name="to-create-an-editor-for-a-vspackage"></a>VSPackage のエディターを作成するには

1. Visual Studio パッケージプロジェクトテンプレートを使用して、カスタムエディターを作成します。

     詳細については、「[チュートリアル: カスタムエディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)」を参照してください。

2. エディターで1つのビューまたは複数のビューをサポートするかどうかを決定します。

     [**新しいウィンドウ**] コマンドをサポートするエディター、またはフォームビューとコードビューがあるエディターでは、個別のドキュメントデータオブジェクトとドキュメントビューオブジェクトが必要です。 1つのビューだけをサポートするエディターでは、ドキュメントデータオブジェクトとドキュメントビューオブジェクトを同じオブジェクトに実装できます。

     複数のビューの例については、「[複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

3. インターフェイスを設定して、エディターファクトリを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> ます。

     詳細については、「[エディターファクトリ](/visualstudio/extensibility/editor-factories?view=vs-2015)」を参照してください。

4. エディターでドキュメントビューのオブジェクトウィンドウを管理するために、埋め込み先でのアクティブ化または簡略化された埋め込みを使用するかどうかを決定します。

     簡略化された埋め込みエディターウィンドウは標準のドキュメントビューをホストし、インプレースアクティベーションエディターウィンドウは ActiveX コントロールまたはその他のアクティブなオブジェクトをドキュメントビューとしてホストします。 詳細については、「簡略化された[埋め込み](../extensibility/simplified-embedding.md)と[インプレースアクティブ化](/visualstudio/misc/in-place-activation?view=vs-2015)」を参照してください。

5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コマンドを処理するインターフェイスを実装します。

6. ドキュメントの永続化と外部ファイルの変更への応答を提供します。

    1. ファイルを永続化するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> エディターのドキュメントデータオブジェクトにおよびを実装します。

    2. 外部ファイルの変更に応答するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> エディターのドキュメントデータオブジェクトにおよびを実装します。

        > [!NOTE]
        > へ `QueryService` の <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> ポインターを取得するには、を呼び出し `IVsFileChangeEx` ます。

7. ドキュメントの編集イベントをソースコード管理で調整します。 次の手順に従います。

    1. でを呼び出して、へのポインターを取得 `IVsQueryEditQuerySave2` `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> します。

    2. 最初の編集イベントが発生したときに、メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> ます。

         このメソッドは、ファイルがまだチェックアウトされていない場合にチェックアウトするようにユーザーに求めます。"ファイルがチェックアウトされていません" 状態を処理して、エラーを回避してください。

    3. 同様に、ファイルを保存する前に、メソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> ます。

         このメソッドは、ファイルが保存されていない場合、または最後の保存以降に変更された場合に、ファイルを保存するようにユーザーに要求します。

8. [**プロパティ**] ウィンドウを有効にすると、エディターで選択したテキストのプロパティを表示できます。 次の手順に従います。

    1. テキスト選択が変更されるたびに <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> を呼び出し、の実装を渡し <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> ます。

    2. `QueryService`サービスで <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> を呼び出して、へのポインターを取得 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> します。

9. ユーザーがエディターと**ツールボックス**の間、または外部エディター (Microsoft Word など) と**ツールボックス**の間で項目をドラッグアンドドロップできるようにします。 次の手順に従います。

    1. エディター `IDropTarget` がドロップ先であることを IDE に警告するには、エディターでを実装します。

    2. エディターが <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> **ツールボックス**内の項目を有効または無効にできるように、ビューにインターフェイスを実装します。

    3. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> およびインターフェイスへのポインターを取得するには、を実装し、サービスに対してを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> ます。

         これらの手順により、VSPackage で**ツールボックス**に新しい項目を追加できるようになります。

10. エディターに他のオプション機能を使用するかどうかを決定します。

    - エディターで検索と置換のコマンドをサポートする場合は、を実装 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget> します。

    - エディターでドキュメントアウトラインツールウィンドウを使用する場合は、を実装 `IVsDocOutlineProvider` します。

    - エディターでステータスバーを使用する場合は、を実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> し、を呼び出して、 `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> へのポインターを取得し `IVsStatusBar` ます。

         たとえば、エディターでは、行または列の情報、選択モード (ストリーム/ボックス)、および挿入モード (insert/上書き) を表示できます。

    - エディターでコマンドをサポートする場合は、 `Undo` OLE 元に戻すマネージャーモデルを使用することをお勧めします。 別の方法として、エディターで直接コマンドを処理することもでき `Undo` ます。

11. VSPackage の Guid、メニュー、エディター、およびその他の機能を含むレジストリ情報を作成します。

     次に、エディターを適切に登録する方法を示すために、 *.rgs*ファイルスクリプトに記述するコードの一般的な例を示します。

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

12. 状況依存のヘルプサポートを実装します。

     この手順では、エディターの項目に対して F1 ヘルプとダイナミックヘルプウィンドウのサポートを提供できます。 詳細については、「[方法: エディターのコンテキストを指定する](/visualstudio/extensibility/how-to-provide-context-for-editors?view=vs-2015)」を参照してください。

13. インターフェイスを実装することによって、エディターからオートメーションオブジェクトモデルを公開し `IDispatch` ます。

     詳細については、「 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)」を参照してください。

## <a name="robust-programming"></a>信頼性の高いプログラミング

- エディターインスタンスは、IDE がメソッドを呼び出したときに作成され <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> ます。 エディターが複数のビューをサポートしている場合は、に `CreateEditorInstance` よってドキュメントデータとドキュメントビューオブジェクトの両方が作成されます。 ドキュメントデータオブジェクトが既に開いている場合は、null 以外の `punkDocDataExisting` 値がに渡され `IVsEditorFactory::CreateEditorInstance` ます。 エディターファクトリの実装では、既存のドキュメントデータオブジェクトに適切なインターフェイスを照会することによって互換性があるかどうかを判断する必要があります。 詳細については、「[複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

- 簡略化された埋め込み方法を使用する場合は、インターフェイスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> ます。

- インプレースライセンス認証を使用する場合は、次のインターフェイスを実装します。

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > この `IOleInPlaceComponent` インターフェイスは、OLE 2 メニューのマージを避けるために使用されます。

   の `IOleCommandTarget` 実装では、**切り取り**、**コピー**、**貼り付け**などのコマンドが処理されます。 を実装する場合 `IOleCommandTarget` 、エディターが独自のコマンドメニュー構造を定義するために独自の*vsct*ファイルを必要とするか、で定義された標準コマンドを実装できるかどうかを決定 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] します。 通常、エディターでは、IDE のメニューを使用して拡張し、独自のツールバーを定義します。 ただし、IDE の標準コマンドセットを使用するだけでなく、エディターで独自の特定のコマンドを定義する必要がある場合もあります。 エディターは、使用する標準コマンドを宣言してから、新しいコマンド、コンテキストメニュー、トップレベルメニュー、ツールバーを*vsct*ファイルで定義する必要があります。 インプレースアクティブ化エディターを作成する場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> OLE 2 メニューのマージではなく、 *vsct*ファイルでエディターのメニューとツールバーを実装して定義します。

- UI でメニューコマンド crowding を回避するには、新しいコマンドをにせよする前に、IDE の既存のコマンドを使用する必要があります。 共有コマンドは、 *Sharedcmddef. vsct*および*shellcmddef. vsct*で定義されています。 これらのファイルは、インストールの VisualStudioIntegration\Common\Inc サブディレクトリに既定でインストールされ [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] ます。

- `ISelectionContainer`では、単一選択と複数選択の両方を表すことができます。 選択した各オブジェクトは、オブジェクトとして実装され `IDispatch` ます。

- IDE は、から `IOleUndoManager` アクセス可能なサービスとして、 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> またはを介してインスタンス化できるオブジェクトとしてを実装し <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> ます。 エディターは、 `IOleUndoUnit` 各アクションのインターフェイスを実装し `Undo` ます。

- カスタムエディターは、次の2つの場所でオートメーションオブジェクトを公開できます。

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>関連項目

- [オートメーションモデルに貢献する](../extensibility/internals/contributing-to-the-automation-model.md)
