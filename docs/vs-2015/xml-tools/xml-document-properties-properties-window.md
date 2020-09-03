---
title: '[XML ドキュメントのプロパティ]、[プロパティ] ウィンドウ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 9dbb34d9-02ea-4201-b445-c98a0eb0d6db
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f620cc2bd189dccf067c6276f760d21cde5cf05e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669518"
---
# <a name="xml-document-properties-properties-window"></a>XML ドキュメント プロパティと [プロパティ] ウィンドウ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **プロパティ** ] ウィンドウには、XML エディターでアクティブになっているドキュメントに関する基本的な情報が表示されます。 使用可能なプロパティは、現在アクティブになっている XML ドキュメントの種類によって異なります。

> [!NOTE]
> XML ドキュメントのプロパティは、すべてソリューション内に保存されます。 このため、ソリューションを次に開いたときにプロパティの値を再入力する必要はありません。

 **エンコード** ファイルの文字エンコーディング。 このプロパティを変更すると、XML 宣言の encoding 属性も変更されます。逆に、encoding 属性を変更すれば、このプロパティも変更されます。 新しいエンコードは、ファイルを保存する際にファイルをエンコードするために使用されます。

 **入力** XSLT スタイルシートに関連付けられている入力ドキュメント。 これは、 **Showxslt 出力** コマンドによって使用されます。 ドキュメントは、参照 ( **[...]** ) ボタンを使用して選択できます。

 このプロパティが表示されるのは、XSLT ファイルが現在エディター ウィンドウでアクティブになっている場合のみになります。

 **出力** XML ドキュメントを変換するときに生成されるファイル。

 ファイルが指定されていない場合は、ファイル拡張子を決定する `method` 要素の `xsl:output` 属性に基づいて既定のファイル名が生成されます。 既定のファイルは、現在のユーザーの一時ディレクトリに置かれます。

 **スキーマ** 検証に使用するスキーマ。 このボタンは、希望のスキーマを選択するために使用する **[XSD Schemas]\(XSD スキーマ\)** ダイアログ ボックスを開きます。

 スキーマへのパスを入力することもできます。 複数のスキーマを指定する場合は、スキーマのパスをそれぞれ二重引用符で囲む必要があります。

 **スタイルシート** [ **Xslt 出力の表示** ] コマンドが使用されている場合に、ドキュメントを変換するために使用される xslt ファイル。 [ **XSLT 出力の表示** ] コマンドを使用したときにこのフィールドが空白の場合、エディターはドキュメントの処理命令で指定された値を使用 `xml-stylesheet` するか、ファイル名の入力を求めます。

 XSLT ファイルを編集するときに、このプロパティを使用して、[ **Xslt 出力の表示** ] または [ **xslt のデバッグ** ] コマンドを選択したときに別のスタイルシートを使用するように指定できます。 たとえば、親のスタイル シートにインクルードされるスタイル シートを編集しているときに、そのように指定することができます。

## <a name="see-also"></a>参照
 [Xml エディター](../xml-tools/xml-editor.md)の [Xml エディターのコンポーネント](../xml-tools/xml-editor-components.md)
