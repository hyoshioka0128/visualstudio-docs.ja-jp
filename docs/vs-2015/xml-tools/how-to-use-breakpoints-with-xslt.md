---
title: '方法: XSLT でブレークポイントを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: bf7bbc2c-71dc-4cac-a6fc-add6b27d92ed
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0519c3ab19e7d36aa26ea2f462c8a4571b9f8b32
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656309"
---
# <a name="how-to-use-breakpoints-with-xslt"></a>方法 : XSLT でブレークポイントを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XSLT スタイル シート内または XML ソース ドキュメント内でブレークポイントを設定することができます。 タグにブレークポイントを設定した場合は、実行の開始時に、ソース行情報を含む次のステートメントにブレークポイントが移動します。

 詳細については、「 [デバッグの基本: ブレークポイント](https://msdn.microsoft.com/752a02c2-0ac7-4c8b-aa1b-4b2b3b21152e)」を参照してください。

## <a name="set-a-breakpoint-in-a-style-sheet"></a>スタイル シート内にブレークポイントを設定する
 XSLT スタイル シートでは、開始タグ、終了タグ、およびテキスト ノードにブレークポイントを設定できます。 スクリプト ブロック内のコードにブレークポイントを設定することもできます。

#### <a name="to-set-a-breakpoint-in-a-style-sheet"></a>スタイル シート内にブレークポイントを設定するには

1. XML エディターでスタイル シートを開きます。

2. ブレークポイントの位置にカーソルを置き、右クリックして [ **ブレークポイント**] をポイントし、[ **ブレークポイントの挿入**] をクリックします。

3. ドキュメントのプロパティウィンドウの [**入力**] フィールドで、参照ボタン ([.**..**]) をクリックします。

4. XML ソースドキュメントを見つけて、[ **開く**] をクリックします。

     これで、XSLT 変換のために使用されるソース ドキュメント ファイルが設定されます。

5. XML エディターのツールバーにある [ **XSL のデバッグ** ] ボタンをクリックします。

## <a name="set-a-breakpoint-in-an-xml-source-document"></a>XML ソース ドキュメント内にブレークポイントを設定する
 XML ソース ドキュメントでは、要素、属性、名前空間ノード、コメント、処理命令、およびテキスト ノードにブレークポイントを設定できます。 ドキュメント ノード、または、親要素から継承された名前空間ノードにブレークポイントを設定することはできません。

#### <a name="to-set-a-breakpoint-in-an-xml-source-document"></a>XML ソース ドキュメント内にブレークポイントを設定するには

1. XML エディターで XML ドキュメントを開きます。

2. ブレークポイントの位置にカーソルを置き、右クリックして [ **ブレークポイント**] をポイントし、[ **ブレークポイントの挿入**] をクリックします。

3. ドキュメントのプロパティウィンドウの [**スタイルシート**] フィールドで、参照ボタン ([.**..**]) をクリックします。

4. XML ソースドキュメントを見つけて、[ **開く**] をクリックします。

     これで、XSLT 変換のために使用されるソース ドキュメント ファイルが設定されます。

5. XML エディターのツールバーにある [ **XSL のデバッグ** ] ボタンをクリックします。

## <a name="see-also"></a>参照
 [チュートリアル: XSLT スタイルシートのデバッグ](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md)
