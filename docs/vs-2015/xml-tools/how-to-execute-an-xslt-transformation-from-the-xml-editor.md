---
title: '方法: XML エディターから XSLT 変換を実行する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4b305d88779603b374e5f95842d7a5271a657268
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666532"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>方法: XML エディターから XSLT 変換を実行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML エディターでは、XSLT スタイル シートを XML ドキュメントと関連付けて変換を実行し、結果を表示させることができます。 XSLT 変換から得られた結果の出力は、新しいドキュメント ウィンドウに表示されます。

 **Output** プロパティでは、出力のファイル名を指定します。 **Output** プロパティが空白の場合は、一時ディレクトリ内にファイル名が生成されます。 ファイル拡張子はスタイル シート内の `xsl:output` 要素に基づき、.xml、.txt、または .htm のいずれかが付けられます。

 **出力**プロパティで .htm または .html 拡張子の付いたファイル名を指定すると、Internet Explorer を使用して XSLT 出力がプレビューされ [!INCLUDE[msCoName](../includes/msconame-md.md)] ます。 他のファイル拡張子はすべて、[!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio によって選択されている既定のエディターを使用して開かれます。 たとえば、ファイル拡張子が .xml の場合、Visual Studio では XML エディターが使用されます。

### <a name="to-execute-an-xslt-transformation-from-an-xml-document"></a>XML ドキュメントから XSLT 変換を実行するには

1. XML エディターで XML ドキュメントを開きます。

2. XSLT スタイル シートを XML ドキュメントと関連付けます。

    - XML ドキュメントに `xml-stylesheet` 処理命令を追加します。 たとえば、ドキュメントのプロローグに `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>` という行を追加します。

         \- または -

    - **[プロパティ]** ウィンドウを使用して、XSLT スタイル シートを追加します。 ドキュメントの**プロパティウィンドウ**で、[**スタイルシート**] フィールドの**参照**ボタンをクリックし、XSLT スタイルシートを選択して、[**開く**] をクリックします。

3. **XML エディター**のツールバーの [ **show xsl Output** ] ボタンをクリックします。

    > [!NOTE]
    > XML ドキュメントに関連付けられているスタイル シートがない場合は、使用するスタイル シートの指定を求めるダイアログ ボックスが表示されます。
    >
    >  XSLT 変換から得られた結果の出力は、新しいドキュメント ウィンドウに表示されます。

### <a name="to-execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>XSLT スタイル シートから XSLT 変換を実行するには

1. XML エディターで XSLT スタイル シートを開きます。

2. ドキュメントの **[プロパティ]** ウィンドウの **[入力]** フィールドで、XML ドキュメントを指定します。

    > [!NOTE]
    > この XML ドキュメントは、変換に使用する入力ドキュメントです。 XSLT 変換の開始時にドキュメントが指定されていない場合、[ **ファイルを開く** ] ダイアログボックスが表示され、その時点でドキュメントを指定できます。

3. **XML エディター**のツールバーの [ **showxslt 出力**] ボタンをクリックします。

     XSLT 変換から得られた結果の出力は、新しいドキュメント ウィンドウに表示されます。

### <a name="to-provide-a-different-output-file-name"></a>異なる出力ファイル名を指定するには

1. ドキュメントの [**プロパティ**] ウィンドウの [**出力**] フィールドで、ファイル名を指定します。

2. **XML エディター**のツールバーの [ **showxslt 出力**] ボタンをクリックします。

     XSLT 変換からの結果の出力は、新しいドキュメントウィンドウに表示されます。出力ウィンドウで使用されるエディターは、 **出力** ドキュメントプロパティのファイル拡張子によって異なります。

## <a name="see-also"></a>参照
 [XML エディター](../xml-tools/xml-editor.md)
