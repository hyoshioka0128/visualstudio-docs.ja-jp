---
title: Visual Studio 2019 SDK の新機能 |マイクロソフトドキュメント
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 187d3df4b5bcefefc0135c010c7d98951e9b3af8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740403"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK の新機能

Visual Studio SDK には、Visual Studio 2019 の次の新機能と更新された機能があります。

## <a name="synchronously-autoloaded-extensions-warning"></a>同期的に自動ロードされた拡張機能の警告

インストールされている拡張機能のいずれかが起動時に同期的に自動ロードされている場合、ユーザーに警告が表示されるようになりました。 警告の詳細については、「[同期的に自動読み込まれた拡張機能](synchronously-autoloaded-extensions.md)」を参照してください。

## <a name="single-unified-visual-studio-sdk"></a>単一の統一されたビジュアル スタジオ SDK

単一の NuGet パッケージを使用してすべての Visual Studio [SDK](https://www.nuget.org/packages/microsoft.visualstudio.sdk)資産を取得できるようになりました。

## <a name="editor-registration-enhancements"></a>編集者登録の機能強化

Visual Studio は、作成後、カスタム エディターの登録をサポートしており、エディターは特定の拡張機能 (たとえば、.xaml や .rc) に対するアフィニティを宣言したり、任意の拡張機能 (.*) に適している場合があります。 Visual Studio 2019 バージョン 16.1 以降では、エディター登録のサポートが広がっています。

### <a name="filenames"></a>ファイル名

特定のファイル拡張子のサポートを登録するだけでなく、エディターは、新しい`ProvideEditorFilename`属性をエディターのパッケージに適用することで、特定のファイル名をサポートするように登録できます。

たとえば、すべての .json ファイルをサポートするエディターは、`ProvideEditorExtension`この属性をパッケージに適用します。

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

16.1 以降、MyEditor が 2 つの既知の .json ファイルのみをサポートしている場合、`ProvideEditorFilename`代わりにこれらの属性をパッケージに適用できます。

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UI コンテキスト

エディターは、有効にした場合を表す 1 つ以上の UI コンテキストを登録できます。 UIContext は、エディターを登録するパッケージに 1`ProvideEditorUIContextAttribute`つ以上のインスタンスを適用することによって登録されます。

エディターに UI コンテキストが登録されている場合:

- 指定された拡張子を持つファイルを開いたときに、登録されている UIContexts が少なくとも 1 つアクティブな場合、エディターはエディター検索に含まれます。
- 登録された UIContext がどれもアクティブでない場合、エディターはエディター検索に含まれません。

エディターが UIContext を登録しない場合は、その拡張機能のエディター検索に常に含まれます。

たとえば、C# プロジェクトが開いているときにのみエディターを使用できる場合、属性を適用してこのアフィニティを`ProvideEditorUIContext`宣言できます。

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
