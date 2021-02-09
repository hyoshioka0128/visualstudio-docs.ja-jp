---
title: 'チェックリスト: 従来の言語サービスを作成する |Microsoft Docs'
description: Visual Studio コアエディターのレガシ言語サービスを作成するために必要な基本手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- language services, native code
ms.assetid: 8b73b341-a33a-4ab5-9390-178c9e563d2d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 823d46453ac6ad4a1a5a42c1f7d18a079b39d12d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99905861"
---
# <a name="checklist-create-a-legacy-language-service"></a>チェックリスト: 従来の言語サービスを作成する
次のチェックリストは、コアエディターの言語サービスを作成するために実行する必要がある基本的な手順の概要を示して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] います。 言語サービスをに統合するには [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、デバッグ式エバリュエーターを作成する必要があります。 詳細については、「 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)で[CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)」を参照してください。

## <a name="steps-to-create-a-language-service"></a>言語サービスを作成する手順

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> インターフェイスを実装します。

    - VSPackage で、 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 言語サービスを提供するためのインターフェイスを実装します。

    - 実装の統合開発環境 (IDE) で言語サービスを使用できるように <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> します。

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>Main language service クラスにインターフェイスを実装します。

     <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>インターフェイスは、コアエディターと言語サービスの間の対話の開始点です。

### <a name="optional-features"></a>オプション機能
 次の機能は省略可能であり、任意の順序で実装できます。 これらの機能により、言語サービスの機能が向上します。

- 構文の色分け表示

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> インターフェイスを実装します。 このインターフェイスの実装では、パーサー情報を使用して適切な色情報を返す必要があります。

  メソッドは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A> インターフェイスを返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ます。 テキストバッファーごとに個別の colorizer インスタンスが作成されるため、インターフェイスを個別に実装する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ます。 詳細については、「 [従来の言語サービスの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)表示」を参照してください。

- [コード ウィンドウ]

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>新しいコードウィンドウが作成されたときに、言語サービスが通知を受け取ることができるように、インターフェイスを実装します。

  メソッドは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetCodeWindowManager%2A> インターフェイスを返し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> ます。 言語サービスは、のコードウィンドウに特殊な UI を追加でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.AddAdornments%2A> ます。 言語サービスでは、でテキストビューフィルターを追加するなど、特別な処理を行うこともでき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager.OnNewView%2A> ます。

- テキストビューフィルター

  言語サービスで IntelliSense ステートメント入力候補を提供するには、テキストビューで処理されるコマンドの一部をインターセプトする必要があります。 これらのコマンドをインターセプトするには、次の手順を実行します。

  - <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コマンドチェーンに参加し、エディターのコマンドを処理するには、を実装します。

  - メソッドを呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 実装を渡し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。

  - <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RemoveCommandFilter%2A>ビューからデタッチするときにメソッドを呼び出して、これらのコマンドが渡されないようにします。

  処理する必要があるコマンドは、提供されているサービスによって異なります。 詳細については、「 [言語サービスフィルターの重要なコマンド](../../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。

  > [!NOTE]
  > インターフェイスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> インターフェイスと同じオブジェクトに実装する必要があり <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。

- ステートメント入力候補

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> インターフェイスを実装します。

  ステートメント入力候補コマンド (つまり、) をサポートし、インターフェイスの <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> メソッドを呼び出して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateCompletionStatus%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 、インターフェイスを渡し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompletionSet> ます。 詳細については、「 [従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。

- メソッドのヒント

  インターフェイスを実装して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodData> 、メソッドのヒントウィンドウにデータを提供します。

  テキストビューフィルターをインストールして、コマンドを適切に処理します。これにより、メソッドのデータヒントウィンドウをいつ表示するかがわかります。 詳細については、「 [従来の言語サービスのパラメーターヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)」を参照してください。

- エラーマーカー

  <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> インターフェイスを実装します。

  インターフェイスを実装するエラーマーカーオブジェクトを作成 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> し、メソッドを呼び出して <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> 、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> エラーマーカーオブジェクトのインターフェイスを渡します。

  通常、各エラーマーカーは、[タスク一覧] ウィンドウの項目を管理します。

- タスク一覧の項目

  インターフェイスを提供するタスク項目クラスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskItem> します。

  インターフェイスとインターフェイスを提供するタスクプロバイダークラスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskProvider2> ます。

  インターフェイスを提供するタスク列挙子クラスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumTaskItems> します。

  タスクプロバイダーをタスク一覧のメソッドに登録し <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RegisterTaskProvider%2A> ます。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>サービス GUID を使用して言語サービスのサービスプロバイダーを呼び出すことによって、インターフェイスを取得し <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> ます。

  タスク項目オブジェクトを作成し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList.RefreshTasks%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> 新規または更新されたタスクがある場合は、インターフェイスでメソッドを呼び出します。

- タスク項目のコメント化

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens> コメントタスクトークンを取得するには、インターフェイスとインターフェイスを使用します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo>サービスからインターフェイスを取得 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> します。

  <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumCommentTaskTokens>メソッドからインターフェイスを取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommentTaskInfo.EnumTokens%2A> します。

  インターフェイスを実装して <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskListEvents> 、トークンリストの変更をリッスンします。

- アウトライン

  アウトラインをサポートするには、いくつかのオプションがあります。 たとえば、[ **定義に折りたたむ** ] コマンドをサポートしたり、エディターで制御されるアウトライン領域を指定したり、クライアント制御領域をサポートしたりできます。 詳細については、「 [方法: 従来の言語サービスで拡張されたアウトラインサポートを提供する](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)」を参照してください。

- 言語サービスの登録

  言語サービスを登録する方法の詳細については、「 [従来の言語サービスを登録](../../extensibility/internals/registering-a-legacy-language-service2.md) する」および「 [vspackage を管理](../../extensibility/managing-vspackages.md)する」を参照してください。

- 状況依存のヘルプ

  次のいずれかの方法で、エディターにコンテキストを提供します。

  - インターフェイスを実装して、テキストマーカーのコンテキストを指定 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> します。

  - インターフェイスを実装して、すべてのユーザーコンテキストを指定 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> します。

## <a name="see-also"></a>関連項目
- [従来の言語サービスを開発する](../../extensibility/internals/developing-a-legacy-language-service.md)
- [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
