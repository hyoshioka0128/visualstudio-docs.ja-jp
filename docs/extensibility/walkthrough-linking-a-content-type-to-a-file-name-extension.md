---
title: コンテンツタイプをファイル名拡張子にリンクする
description: このチュートリアルでは、エディター Managed Extensibility Framework の拡張機能を使用して、独自のコンテンツタイプをファイル名拡張子にリンクする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 990f10fe82b9230c12ba13d736750f2f644c3ee5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078449"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>チュートリアル: コンテンツの種類をファイル名拡張子にリンクする
エディター Managed Extensibility Framework (MEF) 拡張機能を使用して、独自のコンテンツの種類を定義し、ファイル名拡張子をリンクすることができます。 場合によっては、言語サービスによってファイル名の拡張子が既に定義されていることがあります。 ただし、MEF で使用するには、コンテンツの種類にリンクする必要があります。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `ContentTypeTest` します。

2. **Source.extension.vsixmanifest** ファイルで、[**資産**] タブにアクセスし、[**種類**] フィールドを [ **VisualStudio**] に、[**ソース**] フィールドを [現在の **ソリューションのプロジェクト**] に、[**プロジェクト**] フィールドをプロジェクトの名前に設定します。

## <a name="define-the-content-type"></a>コンテンツの種類を定義する

1. クラス ファイルを追加し、その名前を `FileAndContentTypes`にします。

2. 次のアセンブリへの参照を追加します。

    1. System.ComponentModel.Composition

    2. VisualStudio. Logic

    3. VisualStudio. CoreUtility

3. 次のディレクティブを追加 `using` します。

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

5. このクラスでは、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> "hid" という名前のをエクスポートし、その基本定義を "text" に宣言します。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>ファイル名拡張子をコンテンツタイプにリンクする

- このコンテンツの種類をファイル名拡張子にマップするには、 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> 拡張子が *hid* でコンテンツタイプが "hid" のをエクスポートします。

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

## <a name="add-the-content-type-to-an-editor-export"></a>エディターのエクスポートにコンテンツの種類を追加する

1. エディター拡張機能を作成します。 たとえば、「 [チュートリアル: 余白グリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)」で説明されている余白グリフ拡張機能を使用できます。

2. この手順で定義したクラスを追加します。

3. 拡張クラスをエクスポートするときに、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "hid" 型のを追加します。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>こちらもご覧ください
- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
