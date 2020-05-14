---
title: 言語サービスを拡張してエディター構成をサポート
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699584"
---
# <a name="supporting-editorconfig-for-your-language-service"></a>言語サービスのサポート エディター構成

[EditorConfig](https://editorconfig.org/)ファイルを使用すると、プロジェクトごとにインデント サイズなどの一般的なテキスト エディター オプションを記述できます。 Visual Studio の EditorConfig ファイルのサポートの詳細については[、「EditorConfig を使用してポータブル エディター設定を作成](../ide/create-portable-custom-editor-options.md)する」を参照してください。

ほとんどの場合、Visual Studio 言語サービスを実装するとき、EditorConfig ユニバーサル プロパティをサポートするための追加の作業は必要ありません。 ユーザーがファイルを開くと、コア エディターが .editorconfig ファイルを自動的に検出して読み込み、適切なテキスト バッファーとビュー オプションを設定します。 ただし、タブやスペースなどの編集の場合、一部の言語サービスでは、グローバル設定を使用するのではなく、適切なコンテキストテキスト表示オプションを使用することを選択します。 そのような場合は、EditorConfig ファイルをサポートするように言語サービスを更新する必要があります。

以下は、言語サービスを更新して EditorConfig ファイルをサポートするために必要な変更で、グローバル_言語固有の_オプションをコンテキスト オプションに置き換えることにより行_われます_。

## <a name="indent-style"></a>インデント スタイル

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.fInsertTabs<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs|!textBufferOptions.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)<br/>!textView.Options.GetOptionValue(DefaultOptions.ConvertTabsToSpacesOptionId)

## <a name="indent-size"></a>[インデント サイズ]

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uIndentSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.IndentSize|textBufferOptions.GetOptionValue(DefaultOptions.IndentSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.IndentSizeOptionId)

## <a name="tab-size"></a>[タブ サイズ]

言語固有のオプション | コンテキスト オプション
-------|--------
Microsoft.VisualStudio.TextManager.Interop.LANGPREFERENCES.uTabSize<br/>Microsoft.VisualStudio.Package.LanguagePreferences.InsertTabs.TabSize|textBufferOptions.GetOptionValue(DefaultOptions.TabSizeOptionId)<br/>textView.Options.GetOptionValue(DefaultOptions.TabSizeOptionId)

## <a name="see-also"></a>関連項目

- [エディター構成を使用してポータブル エディター設定を作成します。](../ide/create-portable-custom-editor-options.md)
- [エディターおよび言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)
