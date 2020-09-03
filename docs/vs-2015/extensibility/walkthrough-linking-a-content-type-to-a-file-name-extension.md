---
title: 'チュートリアル: コンテンツの種類をファイル名拡張子にリンクする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: beae9d0526cb9f2f294f2267a8da52d3ce3d8c08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201993"
---
# <a name="walkthrough-linking-a-content-type-to-a-file-name-extension"></a>チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

独自のコンテンツの種類を定義し、エディター Managed Extensibility Framework (MEF) 拡張機能を使用してファイル名拡張子をリンクすることができます。 場合によっては、ファイル名拡張子が言語サービスによって既に定義されていることがあります。それでも MEF で使用する場合は、コンテンツの種類にリンクする必要があります。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `ContentTypeTest` します。  
  
2. **Source.extension.vsixmanifest**ファイルで、[**資産**] タブにアクセスし、[**種類**] フィールドを [ **VisualStudio**] に、[**ソース**] フィールドを [現在の**ソリューションのプロジェクト**] に、[**プロジェクト**] フィールドをプロジェクトの名前に設定します。  
  
## <a name="defining-the-content-type"></a>コンテンツの種類の定義  
  
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
  
## <a name="linking-a-file-name-extension-to-a-content-type"></a>コンテンツタイプへのファイル名拡張子のリンク  
  
- このコンテンツの種類をファイル名拡張子にマップするには、 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> 拡張子 ". hid" とコンテンツタイプ "hid" を持つをエクスポートします。  
  
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
  
## <a name="adding-the-content-type-to-an-editor-export"></a>エディターエクスポートへのコンテンツタイプの追加  
  
1. エディター拡張機能を作成します。 たとえば、「 [チュートリアル: 余白グリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)」で説明されている余白グリフ拡張機能を使用できます。  
  
2. この手順で定義したクラスを追加します。  
  
3. 拡張クラスをエクスポートするときに、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "hid" 型のを追加します。  
  
    ```csharp  
    [Export]  
    [ContentType("hid")]  
    ```  
  
## <a name="see-also"></a>参照  
 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
