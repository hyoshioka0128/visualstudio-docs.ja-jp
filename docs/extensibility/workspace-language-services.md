---
title: Visual Studio のワークスペースと言語サービス |Microsoft Docs
description: 言語サービスが、ソリューションやプロジェクトを操作するときに使用されるものと同じ機能を備えた、オープンフォルダーのユーザーを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 815cfb9e17fed38b519719010acd997f7fdc5242
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877040"
---
# <a name="workspaces-and-language-services"></a>ワークスペースと言語サービス

言語サービスでは、ソリューションやプロジェクトを操作するときに使用するのと同じ豊富な言語機能を、開いている [フォルダー](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) ユーザーに提供できます。 言語サービスは、開いているドキュメントのファイル拡張子またはコンテンツに基づいて自己アクティブ化することができます。ただし、この "緩いファイル" 言語サービスは構文の強調表示に限定されます。 ソースコードを編集または確認するときに、より高度なエクスペリエンスを提供するには、追加情報が必要です。 各言語サービスには、ドキュメントのこの追加コンテキストデータを使用して初期化するための独自の API が用意されています。 通常、これはプロジェクトシステムによって管理され、言語サービスとビルドシステムの両方に密結合されます。

## <a name="initialization"></a>初期化

[ワークスペース](workspaces.md)では、言語サービスは、 <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> その言語サービスのみを専門とし、ビルド作成の何も認識しない拡張ポイントによって初期化されます。 このようにして、言語サービスの所有者は、ビルド中にコンパイラを実行するためのフォルダーとファイル内のパターンの数に関係なく、1つの開いているフォルダーの拡張機能を維持できます (たとえば、MSBuild やメイクファイルなど)。 ファイルコンテキストが作成されたファイルがディスク上で変更され、ファイルコンテキストが更新されると、更新されたファイルコンテキストのセットが言語サービスプロバイダーに通知されます。 言語サービスプロバイダーは、そのモデルを更新できます。

エディターでドキュメントが開かれている場合、Visual Studio では、一致するファイルコンテキストプロバイダーが見つかるファイルコンテキストの種類を必要とする言語サービスプロバイダーのみが考慮されます。 次に、を使用して、一致するプロバイダーのファイルコンテキストを、選択した言語サービスプロバイダーに渡し `ILanguageServiceProvider.InitializeAsync` ます。 言語サービスプロバイダーは、そのファイルコンテキストデータを使用して、言語サービスプロバイダーの実装の詳細を示しますが、想定されるユーザーエクスペリエンスは、開いているドキュメントに対してより高度な言語サービスになります。

## <a name="using-ilanguageserviceprovider"></a>ILanguageServiceProvider の使用

言語サービスは、 `ContextType` `SupportedContextTypes` language server export 属性の値のいずれかに一致するを使用してファイルコンテキストが作成されたときに通知されます。

言語サービスをサポートするには、拡張機能に次のものが必要です。

- 一意の `Guid` 。 これは、 `SupportedContextTypes` 属性引数およびオブジェクトで使用され `FileContext` ます。
- 言語ファイルコンテキスト
  - プロバイダーファクトリ
    - `ExportFileContextProviderAttribute`上の属性は、で一意に生成されます。 `Guid``SupportedContextTypes`
    - `IWorkspaceProviderFactory<IFileContextProvider>` を実装します
  - のプロバイダーの実装 `IFileContextProvider.GetContextsForFileAsync`
    - `FileContext`コンストラクター引数を使用し `contextType` て、一意に生成されたとして新しいを構築します。`Guid`
    - のプロパティを使用して `Context` `FileContext` 、追加のデータを `ILanguageServiceProvider`
- 言語サービス
  - プロバイダーファクトリ
    - `ExportLanguageServiceProvider`上の属性は、で一意に生成されます。 `Guid``SupportedContextTypes`
    - `IWorkspaceProviderFactory<ILanguageServiceProvider>` を実装します
  - プロバイダー
    - `ILanguageServiceProvider` を実装します
    - `ILanguageServiceProvider.InitializeAsync`ファイルを開いたときに、指定された引数の言語サービスを有効にするために使用します
    - `ILanguageServiceProvider.UninitializeAsync`ファイルが閉じられたときに、指定された引数の言語サービスを無効にするには、を使用します。

>[!WARNING]
>これらのメソッドは、 `ILanguageServiceProvider` メインスレッドのワークスペースによって呼び出されることがあります。 UI の遅延が発生しないように、別のスレッドで作業をスケジュールすることを検討してください。

## <a name="language-server-protocol"></a>言語サーバー プロトコル

Api は、 `Microsoft.VisualStudio.Workspace.*` 開いているフォルダーで言語サービスを有効にする唯一の方法ではありません。 別の方法として、言語サーバーを使用することもできます。 詳細については、 [言語サーバープロトコル](language-server-protocol.md)に関する説明を参照してください。

## <a name="related-interfaces"></a>関連インターフェイス

- <xref:Microsoft.VisualStudio.Workspace.Intellisense.ILanguageServiceProvider> は、ファイルの種類が一致するファイルが開かれているか、編集のために閉じられたときに呼び出されます。

## <a name="next-steps"></a>次のステップ

* [ワークスペースビルド](workspace-build.md) -オープンフォルダーは、MSBuild やメイクファイルなどのビルドシステムをサポートします。