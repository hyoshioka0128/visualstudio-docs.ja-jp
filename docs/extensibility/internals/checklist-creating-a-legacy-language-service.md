---
title: 'チェックリスト: 従来の言語サービスを作成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11785dab63cbb6a95ab2d34c5edbfb4525ebf34c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709788"
---
# <a name="checklist-create-a-legacy-language-service"></a>チェックリスト: 従来の言語サービスを作成する
次のチェックリストは、コア エディターの言語サービスを作成するために実行する必要がある基本的な[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]手順をまとめたものです。 言語サービスを に[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合するには、デバッグ式エバリュエーターを作成する必要があります。 詳細については、「 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)で[CLR 式エバリュエーターを記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)する 」を参照してください。

## <a name="steps-to-create-a-language-service"></a>言語サービスを作成する手順

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> インターフェイスを実装します。

    - VSPackage で、言語サービス<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>を提供するインターフェイスを実装します。

    - 実装内の統合開発環境 (IDE) で言語サービスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>使用できるようにします。

2. メイン言語<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>サービス クラスでインターフェイスを実装します。

     インターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>は、コア エディターと言語サービス間の対話の開始点です。

### <a name="optional-features"></a>オプション機能
 次の機能はオプションで、任意の順序で実装できます。 これらの機能により、言語サービスの機能が向上します。

- 構文の色分け表示

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装します。 このインターフェイスの実装では、パーサー情報が適切な色情報を返す必要があります。

  この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>メソッドはインターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>を返します。 テキスト バッファーごとに個別のカラー化インスタンスが作成されるため、インターフェイスを個別に<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>実装する必要があります。 詳細については、「[従来の言語サービスでの構文の色付け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)」を参照してください。

- [コード ウィンドウ]

  新しい<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>コード ウィンドウが作成されたときに通知を受け取る言語サービスを有効にするインターフェイスを実装します。

  この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A>メソッドはインターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>を返します。 その後、言語サービスは、 の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A>コード ウィンドウに特別な UI を追加できます。 言語サービスは、テキスト ビュー フィルタを に追加するなど、あらゆる特別な<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A>処理を行うこともできます。

- テキスト ビュー フィルター

  言語サービスで IntelliSense ステートメントの補完を提供するには、テキスト ビューがそれ以外で処理するコマンドの一部をインターセプトする必要があります。 これらのコマンドを代行受信するには、以下の手順を実行します。

  - コマンド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>チェーンに参加し、エディタ コマンドを処理する実装。

  - メソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>呼び出し、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実装を渡します。

  - これらのコマンド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A>が渡されないように、ビューからデタッチするときにメソッドを呼び出します。

  処理する必要があるコマンドは、提供されるサービスによって異なります。 詳細については、「[言語サービス フィルタの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。

  > [!NOTE]
  > インターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>は、インターフェイスと同じオブジェクトに実装する<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>必要があります。

- ステートメント入力候補

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> インターフェイスを実装します。

  ステートメント完了コマンド (つまり) を<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>サポートし、インターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A>でメソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>呼び出して<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet>、インターフェイスを渡します。 詳細については、「[レガシ言語サービスでのステートメントの入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。

- メソッドのヒント

  メソッド<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData>ヒント ウィンドウのデータを提供するインターフェイスを実装します。

  テキスト ビュー フィルターをインストールしてコマンドを適切に処理し、メソッド データ ヒント ウィンドウを表示するタイミングを確認します。 詳細については、「[従来の言語サービスでのパラメーター情報](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)」を参照してください。

- エラー マーカー

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスを実装します。

  インターフェイスを実装するエラー マーカー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>オブジェクトを作成し<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A>、エラー マーカー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>オブジェクトのインターフェイスを渡してメソッドを呼び出します。

  通常、各エラー マーカーはタスク リスト ウィンドウ内の項目を管理します。

- タスク リスト アイテム

  インターフェイスを提供するタスク項目クラス<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem>を実装します。

  インターフェイスとインターフェイスを提供する<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider>タスク プロバイダー<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2>クラスを実装します。

  インターフェイスを提供するタスク列挙子<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems>クラスを実装します。

  タスク リストの<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A>メソッドにタスク プロバイダーを登録します。

  サービス<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>GUID<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>を使用して言語サービスのサービス プロバイダを呼び出して、インターフェイスを取得します。

  タスク アイテム オブジェクトを<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A>作成し、新<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>しいタスクまたは更新されたタスクがある場合は、インターフェイスでメソッドを呼び出します。

- タスク アイテムのコメント

  インターフェイスと<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>インターフェイスを使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>して、コメント タスク トークンを取得します。

  サービスから<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>インターフェイスを取得<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>します。

  メソッドから<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>インターフェイスを<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A>取得します。

  トークン<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents>リストの変更をリッスンするインターフェイスを実装します。

- アウトライン

  アウトラインをサポートするためのオプションはいくつかあります。 たとえば、[**定義に折りたたむ]** コマンドをサポートしたり、エディター制御のアウトライン領域を提供したり、クライアント制御領域をサポートしたりできます。 詳細については、「[方法 : 従来の言語サービスでの拡張アウトライン サポートの提供](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)」を参照してください。

- 言語サービスの登録

  言語サービスを登録する方法の詳細については、「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service2.md)」および[「VSPackages](../../extensibility/managing-vspackages.md)の管理 」を参照してください。

- 状況依存のヘルプ

  次のいずれかの方法で、エディターにコンテキストを提供します。

  - インターフェイスを実装して、テキスト マーカー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>のコンテキストを提供します。

  - インターフェイスを実装して、すべてのユーザー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>コンテキストを提供します。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
