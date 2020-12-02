---
title: XSLT 変換の実行
description: XML エディターを使用して XSLT スタイルシートを XML ドキュメントに関連付け、XSLT 変換を実行し、出力を表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 56a0fe82-5231-487d-8b6e-a08a9b04e0fc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f1c7165f301c82dfaf5aa066a3e15bd7ab244089
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95970245"
---
# <a name="how-to-execute-an-xslt-transformation-from-the-xml-editor"></a>方法: XML エディターから XSLT 変換を実行する

XML エディターでは、XSLT スタイル シートを XML ドキュメントと関連付けて変換を実行し、結果を表示することができます。 XSLT 変換から得られた結果の出力は、新しいドキュメント ウィンドウに表示されます。

**Output** プロパティでは、出力のファイル名を指定します。 **Output** プロパティが空白の場合は、一時ディレクトリ内にファイル名が生成されます。 ファイル拡張子はスタイル シート内の `xsl:output` 要素に基づき、.*xml*、.*txt* または .*htm* のいずれかが付けられます。

**Output** プロパティで、拡張子が .*htm* または .*html* のファイル名が指定されている場合は、Web ブラウザーを使用して、XSLT 出力のプレビューが行われます。 他のファイル拡張子はすべて、Visual Studio によって選択されている既定のエディターを使用して開かれます。 たとえば、ファイル拡張子が .*xml* の場合、Visual Studio では XML エディターが使用されます。

## <a name="execute-an-xslt-transformation-from-an-xml-file"></a>XML ファイルから XSLT 変換を実行する

1. XML エディターで XML ドキュメントを開きます。

2. XSLT スタイル シートを XML ドキュメントと関連付けます。

    - XML ドキュメントに `xml-stylesheet` 処理命令を追加します。 たとえば、ドキュメントのプロローグに `<?xml-stylesheet type='text/xsl' href='filename.xsl'?>` という行を追加します

       \- または -

    - **[プロパティ]** ウィンドウを使用して、XSLT スタイル シートを追加します。 エディターで XML ファイルを開いた状態で、エディター内の任意の場所を右クリックし、 **[プロパティ]** を選択します。 **[プロパティ]** ウィンドウで **[スタイルシート]** フィールドをクリックし、参照ボタン ([...]) を選択します。XSLT スタイル シートを選択し、 **[開く]** を選択します。

3. メニュー バーで、 **[XML]**  >  **[デバッグなしで XSLT を開始]** を選択します。 または、**Ctrl**+**Alt**+**F5** キーを押します。

   XSLT 変換から得られた出力は、新しいドキュメント ウィンドウに表示されます。

   > [!NOTE]
   > XML ドキュメントに関連付けられているスタイル シートがない場合は、使用するスタイル シートの指定を求めるダイアログ ボックスが表示されます。

## <a name="execute-an-xslt-transformation-from-an-xslt-style-sheet"></a>XSLT スタイル シートから XSLT 変換を実行する

1. XML エディターで XSLT スタイル シートを開きます。

2. ドキュメントの **[プロパティ]** ウィンドウの **[入力]** フィールドで、XML ドキュメントを指定します。

   > [!NOTE]
   > この XML ドキュメントは、変換に使用する入力ドキュメントです。 XSLT 変換が開始されたときにドキュメントが指定されていない場合、 **[ファイルを開く]** ダイアログ ボックスが表示されるので、その時点でドキュメントを指定することができます。

3. メニュー バーで、 **[XML]**  >  **[デバッグなしで XSLT を開始]** を選択します。 または、**Ctrl**+**Alt**+**F5** キーを押します。

   XSLT 変換から得られた出力は、新しいドキュメント ウィンドウに表示されます。

## <a name="specify-an-output-file-name"></a>出力ファイル名を指定する

XML ファイルと XSL ファイルの両方に対して出力ファイル名を指定できます。 **[プロパティ]** ウィンドウを開き、 **[出力]** フィールドでファイル名を指定します。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
