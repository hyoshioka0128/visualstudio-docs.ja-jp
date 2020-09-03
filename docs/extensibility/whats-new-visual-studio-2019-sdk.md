---
title: Visual Studio 2019 SDK の新機能 |Microsoft Docs
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 187d3df4b5bcefefc0135c010c7d98951e9b3af8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740403"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK の新機能

Visual Studio SDK には、Visual Studio 2019 の次の新機能と更新された機能があります。

## <a name="synchronously-autoloaded-extensions-warning"></a>同期的に自動読み込みされる拡張機能の警告

インストールされている拡張機能のいずれかが起動時に同期的に自動で読み込まれた場合、ユーザーに警告が表示されるようになりました。 警告の詳細については、「 [同期的に自動読み込み](synchronously-autoloaded-extensions.md)された拡張機能」を参照してください。

## <a name="single-unified-visual-studio-sdk"></a>単一の統合された Visual Studio SDK

1つの NuGet パッケージ [VisualStudio](https://www.nuget.org/packages/microsoft.visualstudio.sdk)を使用して、すべての VISUAL Studio SDK 資産を取得できるようになりました。

## <a name="editor-registration-enhancements"></a>エディターの登録の機能強化

Visual Studio では、作成以降、特定の拡張機能 (.xaml や .rc など) のアフィニティをエディターが宣言できるカスタムエディター登録がサポートされています。また、任意の拡張機能 (. *) に適しています。 Visual Studio 2019 バージョン16.1 以降では、エディターの登録のサポートが拡大されています。

### <a name="filenames"></a>ファイル名

エディターでは、特定のファイル拡張子のサポートを登録するだけでなく、エディターのパッケージに新しい属性を適用することによって、特定のファイル名をサポートするように登録することもでき `ProvideEditorFilename` ます。

たとえば、すべての json ファイルをサポートするエディターでは、この `ProvideEditorExtension` 属性がパッケージに適用されます。

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

16.1 以降では、MyEditor がいくつかのよく知られた json ファイルのみをサポートしている場合、代わりにこれらの `ProvideEditorFilename` 属性をパッケージに適用できます。

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>の uicontexts の

エディターでは、有効になったときに表す1つ以上の UIContexts を登録できます。 UIContexts は `ProvideEditorUIContextAttribute` 、エディターを登録するパッケージにの1つ以上のインスタンスを適用することによって登録されます。

エディターで UIContexts が登録されている場合は、次のようになります。

- 指定した拡張子を持つファイルを開いたときに、登録されている UIContexts の少なくとも1つがアクティブな場合、エディターはエディターの検索に含まれます。
- 登録されている UIContexts がいずれもアクティブでない場合、エディターはエディターの検索に含まれません。

エディターで UIContexts が登録されていない場合は、常に、その拡張機能を検索するエディターに含まれます。

たとえば、C# プロジェクトが開いているときにのみエディターを使用できる場合は、属性を適用することでこのアフィニティを宣言でき `ProvideEditorUIContext` ます。

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
