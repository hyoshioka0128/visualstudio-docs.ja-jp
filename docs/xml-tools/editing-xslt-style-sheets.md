---
title: XSLT スタイル シートの編集
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 080bed0f-0ca9-4be7-aecd-6bdaebc04007
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 81bab324c58c06cc1ca553bae2f81faf474c4ad0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592842"
---
# <a name="edit-xslt-style-sheets"></a>XSLT スタイル シートの編集

XML エディターは、XSLT スタイル シートの編集にも使用することができます。 IntelliSense、アウトライン、XML スニペットなどの、エディターが備える既定の機能を活用できます。 さらに、XSLT での開発を容易にする新機能もあります。

## <a name="xslt-features"></a>XSLT 機能

XSLT スタイル シートの操作時に固有な機能の説明を次の表に示します。

**構文の色分け表示**

`template` や `match` などの XSLT キーワードは、 **[フォントおよび色]** の設定で指定されている XSLT キーワードの色で表示されます。

**波下線**

XML エディターでは、インストールされた *xslt.xsd* ファイルを使用して XSLT スタイル シートを検証します。 検証エラーは、青色の波下線で表示されます。 XML エディターは、バックグラウンドでスタイル シートのコンパイルも行い、適切な波下線でコンパイラのエラーや警告を通知します。

**スクリプト ブロックのサポート**

スクリプト ブロック内のコードは XSLT デバッガーによってサポートされているので、ブレークポイントを設定してスクリプト ブロックのコードをステップ実行することができます。

**XSLT 出力の表示**

XSL 変換を実行し、XML エディターから出力を参照することができます。 詳細については、[XML エディターから XSLT 変換を実行する](../xml-tools/how-to-execute-an-xslt-transformation-from-the-xml-editor.md)」を参照してください。

**XSLT のデバッグ**

XML エディターでは、XSLT ファイルから XSLT デバッガーを起動できます。 このデバッガーは、XSLT ファイルでのブレークポイントの設定や、XSLT 実行状態の表示などをサポートしています。 XSLT 変数の上にカーソルを置くと、変数の値を示すツール ヒントが表示されます。 このデバッガーを使用すると、スタイル シートのデバッグや、他のアプリケーションから呼び出されたコンパイル済みの XSL 変換のデバッグが可能です。 詳しくは、「[XSLT のデバッグ](../xml-tools/debugging-xslt.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
