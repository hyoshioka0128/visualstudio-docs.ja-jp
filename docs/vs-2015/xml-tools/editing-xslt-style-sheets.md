---
title: XSLT スタイルシートの編集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 080bed0f-0ca9-4be7-aecd-6bdaebc04007
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e1669affa89c91ca3ae1958c22ff3ec4d56bb8c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670963"
---
# <a name="editing-xslt-style-sheets"></a>XSLT スタイル シートの編集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML エディターは、XSLT スタイル シートの編集にも使用することができます。 IntelliSense、アウトライン、XML スニペットなどの、エディターが備える既定の機能を活用できます。 さらに、XSLT での開発を容易にする新機能もあります。

## <a name="xslt-features"></a>XSLT 機能
 XSLT スタイル シートの操作時に固有な機能の説明を次の表に示します。

 **構文の色分け** 、などの XSLT キーワード `template` は、[ `match` **フォントおよび色** ] 設定で指定された xslt キーワードの色で表示されます。

 **波下線** XML エディターは、インストールされた xslt .xsd ファイルを使用して、XSLT スタイルシートを検証します。 検証エラーは、青色の波下線で表示されます。 XML エディターは、バックグラウンドでスタイル シートのコンパイルも行い、適切な波下線でコンパイラのエラーや警告を通知します。

 **スクリプトブロックのサポート** スクリプトブロック内のコードは XSLT デバッガーによってサポートされるため、ブレークポイントを設定し、スクリプトブロックコードをステップ実行できます。

 **XSLT 出力の表示** XSL 変換を実行し、XML エディターから出力を表示することができます。 詳細については、「 [方法: XML エディターから XSLT 変換を実行](../xml-tools/how-to-execute-an-xslt-transformation-from-the-xml-editor.md)する」を参照してください。

 **XSLT のデバッグ** Xslt デバッガーは、XML エディターで XSLT ファイルから起動できます。 このデバッガーは、XSLT ファイルでのブレークポイントの設定や、XSLT 実行状態の表示などをサポートしています。 XSLT 変数の上にカーソルを置くと、変数の値を示すツール ヒントが表示されます。 このデバッガーを使用すると、スタイル シートのデバッグや、他のアプリケーションから呼び出されたコンパイル済みの XSL 変換のデバッグが可能です。 詳しくは、「[XSLT のデバッグ](../xml-tools/debugging-xslt.md)」をご覧ください。

## <a name="see-also"></a>参照
 [XML エディター](../xml-tools/xml-editor.md)
