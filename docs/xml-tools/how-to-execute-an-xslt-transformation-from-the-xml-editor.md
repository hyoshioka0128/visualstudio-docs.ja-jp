---
title: XSLT 変換を実行する
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3bd26eaadf921d13fc425a91031a39df5a80ea2a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592699"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>方法: XML エディターから XSLT 変換を実行する

XML エディターを使用すると、XSLT スタイルシートを XML ドキュメントに関連付けたり、変換を実行したり、出力を表示したりできます。 XSLT 変換から得られた結果の出力は、新しいドキュメント ウィンドウに表示されます。

Output**プロパティは**、出力のファイル名を指定します。 **出力**プロパティが空白の場合は、一時ディレクトリにファイル名が生成されます。 ファイル拡張子は、スタイルシートの `xsl:output` 要素に基づいており、にすることができます。*xml*、。*txt*または。*htm*。

**出力**プロパティがを使用してファイル名を指定している場合。*htm*または。*html*拡張機能では、web ブラウザーを使用して XSLT 出力がプレビューされます。 他のすべてのファイル拡張子は、Visual Studio によって選択された既定のエディターを使用して開きます。 たとえば、ファイル拡張子がの場合です。*xml*、Visual STUDIO は xml エディターを使用します。

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>XML ファイルから XSLT 変換を実行する

1. Xml エディターで XML ドキュメントを開きます。

2. XSLT スタイル シートを XML ドキュメントと関連付けます。

    - XML ドキュメントに `xml-stylesheet` 処理命令を追加します。 たとえば、ドキュメントプロローグに次の行を追加します。 `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>`

       -または-

    - **[プロパティ]** ウィンドウを使用して XSLT スタイルシートを追加します。 エディターで XML ファイルを開いた状態で、エディター内の任意の場所を右クリックし、 **[プロパティ]** を選択します。 **[プロパティ]** ウィンドウで、 **[スタイルシート]** フィールドをクリックし、参照ボタン (...) を選択します。XSLT スタイルシートを選択し、 **[開く]** を選択します。

3. メニューバーで、[ **XML** > **デバッグなしで XSLT を開始**] を選択します。 または、 **Ctrl**+**Alt**+**F5**キーを押します。

   XSLT 変換からの出力が新しいドキュメントウィンドウに表示されます。

   > [!NOTE]
   > XML ドキュメントに関連付けられているスタイル シートがない場合は、使用するスタイル シートの指定を求めるダイアログ ボックスが表示されます。

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>Xslt スタイルシートから XSLT 変換を実行する

1. XML エディターで XSLT スタイルシートを開きます。

2. ドキュメントの **[プロパティ]** ウィンドウの **[入力]** フィールドで、XML ドキュメントを指定します。

   > [!NOTE]
   > この XML ドキュメントは、変換に使用する入力ドキュメントです。 XSLT 変換の開始時にドキュメントが指定されていない場合、 **[ファイルを開く]** ダイアログボックスが表示され、その時点でドキュメントを指定できます。

3. メニューバーで、[ **XML** > **デバッグなしで XSLT を開始**] を選択します。 または、 **Ctrl**+**Alt**+**F5**キーを押します。

   XSLT 変換からの出力が新しいドキュメントウィンドウに表示されます。

## <a name="specify-an-output-file-name"></a>出力ファイル名を指定してください

XML ファイルと XSL ファイルの両方に対して出力ファイル名を指定できます。 **[プロパティ]** ウィンドウを開き、 **[出力]** フィールドにファイル名を指定します。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
