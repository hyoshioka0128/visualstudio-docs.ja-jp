---
title: EditorConfig をサポートするための言語サービスの拡張
ms.date: 11/22/2017
ms.topic: conceptual
helpviewer_keywords:
- editorconfig [extensibility]
- editorconfig, supporting in a language service
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ddfe0e30904d000b4fd70c85371d29a2ee486932
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699584"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>言語サービスの EditorConfig のサポート

[Editorconfig](https://editorconfig.org/) ファイルを使用すると、プロジェクトごとにインデントサイズなどの一般的なテキストエディターオプションを記述できます。 Visual Studio が EditorConfig ファイルをサポートする方法の詳細については、「 [editorconfig を使用してポータブルエディターの設定を作成](../ide/create-portable-custom-editor-options.md)する」を参照してください。

ほとんどの場合、Visual Studio 言語サービスを実装するとき、EditorConfig ユニバーサル プロパティをサポートするための追加の作業は必要ありません。 ユーザーがファイルを開くと、コア エディターが .editorconfig ファイルを自動的に検出して読み込み、適切なテキスト バッファーとビュー オプションを設定します。 ただし、タブやスペースなどの編集では、一部の言語サービスでは、グローバル設定を使用するのではなく、適切なコンテキストテキスト表示オプションを使用することが選択されています。 そのような場合は、EditorConfig ファイルをサポートするように言語サービスを更新する必要があります。

次に、グローバル _言語固有_ のオプションを _コンテキスト_ オプションに置き換えることによって、editorconfig ファイルをサポートするように言語サービスを更新するために必要な変更を示します。

## <a name="indent-style"></a>インデント スタイル

言語固有のオプション | コンテキストオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>[インデント サイズ]

言語固有のオプション | コンテキストオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>[タブ サイズ]

言語固有のオプション | コンテキストオプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>関連項目

- [EditorConfig を使用して移植可能なエディター設定を作成する](../ide/create-portable-custom-editor-options.md)
- [エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)
