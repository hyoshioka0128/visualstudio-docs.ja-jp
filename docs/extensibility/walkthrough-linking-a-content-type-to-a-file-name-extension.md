---
title: 'チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 328be013b5d522938cd7450fc53d4866c632abb3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697086"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする
エディター マネージ機能拡張フレームワーク (MEF) 拡張機能を使用して、独自のコンテンツ タイプを定義し、ファイル名拡張子をリンクできます。 場合によっては、ファイル名拡張子は言語サービスによって既に定義されています。 ただし、MEF で使用するには、コンテンツ タイプにリンクする必要があります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`ContentTypeTest`を付ける:

2. **source.extension.vsixmanifest**ファイルで、[**資産**] タブに移動し、[**種類]** フィールドを **[Microsoft.VisualStudio.MefComponent]** に、[**ソース**] フィールドを **[現在のソリューションのプロジェクト**] に、[**プロジェクト**] フィールドをプロジェクトの名前に設定します。

## <a name="define-the-content-type"></a>コンテンツ タイプの定義

1. クラス ファイルを追加し、その名前を `FileAndContentTypes`にします。

2. 次のアセンブリへの参照を追加します。

    1. System.ComponentModel.Composition

    2. ロジック

    3. ユーティリティ

3. 次`using`のディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 定義を含む静的クラスを宣言します。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. このクラスでは、名前付<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>きの "hid" をエクスポートし、その基本定義を "text" として宣言します。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>ファイル名拡張子をコンテンツ タイプにリンクする

- このコンテンツ タイプをファイル名拡張子にマップするには、拡張子<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>*が .hid*のを持つ をエクスポートし、コンテンツ タイプが "hid" になっている必要があります。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
         [Export]
         [Name("hid")]
         [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;

         [Export]
         [FileExtension(".hid")]
         [ContentType("hid")]
        internal static FileExtensionToContentTypeDefinition hiddenFileExtensionDefinition;
    }
    ```

## <a name="add-the-content-type-to-an-editor-export"></a>コンテンツ タイプをエディター エクスポートに追加する

1. エディター拡張機能を作成します。 たとえば、「チュートリアル: 余白グリフの作成」で説明[されている余白グリフの拡張機能を](../extensibility/walkthrough-creating-a-margin-glyph.md)使用できます。

2. このプロシージャで定義したクラスを追加します。

3. 拡張クラスをエクスポートする場合は、型<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"hid" を追加します。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
