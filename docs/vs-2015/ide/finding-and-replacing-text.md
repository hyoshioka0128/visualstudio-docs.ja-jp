---
title: テキストの検索と置換 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.find
- vs.findreplacecontrol
- vs.findreplace.findsymbol
- vs.findreplace.symbol
- findresultswindow
- vs.findreplace.quickreplace
- vs.findsymbol
- vs.findinfiles
- vs.findresults1
- vs,findsymbolwindow
- vs.findreplace.quickfind
- vs.lookin
- vs.replace
helpviewer_keywords:
- text searches
- Replace in Files dialog box
- find, text
- Find in Files dialog box
- find
- text searches, finding and replacing text
- Replace dialog box
- text, finding and replacing
- find, symbol
- find and replace
- replace
- find text
- replacing text
ms.assetid: a62545c3-1570-4d12-99fb-a82607eb35a1
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 025ba2eb95514efc740d1f8f7b3bf674d6bf237a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645643"
---
# <a name="finding-and-replacing-text"></a>Finding and Replacing Text
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio Code エディターや、 **[検索結果]** ウィンドウなど特定のテキストベースの出力ウィンドウでは、 **[検索と置換]** コントロールまたは **[フォルダーを指定して検索]/[フォルダーを指定して置換]** を使用して、テキストの検索と置換を行うことができます。 検索と置換は、XAML デザイナー、Windows フォーム デザイナー、ツール ウィンドウなどのデザイナー ウィンドウでも実行することができます。

 検索のスコープは、現在のドキュメント、現在のソリューション、またはカスタム フォルダー セットに設定できます。 複数ファイル検索用に、一連のファイル名拡張子を指定することもできます。 .NET 正規表現を使用すると、検索構文をカスタマイズできます。

 正規表現で検索と置換を行う方法については、「[Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

> [!TIP]
> **[検索]** ボックスは、ツール バー コントロールとして使用できますが、既定では表示されません。 **[標準]** ツール バーの **[ボタンの追加または削除]** を選択し、 **[検索]** を選択すると、 **[検索]** ボックスを表示できます。 詳細については、「[[検索] ボックス](../ide/find-command-box.md)」を参照してください。

## <a name="find-and-replace-control"></a>[検索と置換] コントロール
 **[検索と置換]** コントロールは、コード エディター ウィンドウの右上隅に表示されます。 **[検索と置換]** コントロールにより、現在のドキュメントに出現する指定された検索文字列がすべて直ちに強調表示されます。 検索コントロールの **[次を検索]** または **[前を検索]** をクリックすると、1 つの出現箇所から別の出現箇所に移動できます。

 **[検索]** ボックスの横にあるボタンをクリックして、置換オプションにアクセスすることもできます。 置換を 1 か所ずつ実行するには、 **[置換]** ボックスの横にある **[次を置換]** をクリックします。 すべての一致項目を置換するには、 **[すべて置換]** をクリックします。

 一致項目の強調表示色を変更するには、 **[ツール]** メニューで **[オプション]** 、 **[環境]** 、 **[フォントおよび色]** の順にクリックします。 **[設定の表示]** の一覧で **[テキスト エディター]** をクリックし、 **[表示項目]** の一覧で **[蛍光ペンの検索]** (拡張機能) をクリックします。

### <a name="searching-tool-windows"></a>ツール ウィンドウでの検索
 **[検索]** コントロールは、 **[出力]** ウィンドウや **[検索結果]** ウィンドウなどのコード ウィンドウまたはテキスト ウィンドウでも使用できます。これには、 **[編集]** メニューの **[検索と置換]** をクリックするか、Ctrl キーを押しながら F キーを押します。

 一部のツール ウィンドウで使用できるバージョンの [検索] コントロールもあります。 たとえば、検索ボックスにテキストを入力することにより、 **[ツールボックス]** ウィンドウに表示されるコントロールの一覧をフィルター処理できるようになりました。 コンテンツを検索できる他のツール ウィンドウとしては、**ソリューション エクスプローラー**、 **[プロパティ]** ウィンドウ、**チーム エクスプローラー**などがあります。

## <a name="findreplace-in-files"></a>[フォルダーを指定して検索]/[フォルダーを指定して置換]
 **[フォルダーを指定して検索]/[フォルダーを指定して置換]** は **[検索と置換]** コントロールと同様に動作します。ただし、検索のスコープを定義できる点が異なります。 エディター内で開いているファイルを検索するだけでなく、開いているすべてのドキュメント、ソリューション全体、現在のプロジェクト、および選択したフォルダー セットを対象にして検索できます。 また、ファイル名拡張子によって検索することもできます。 **[フォルダーを指定して検索]/[フォルダーを指定して置換]** ダイアログ ボックスにアクセスするには、 **[編集]** メニューの **[検索と置換]** をクリックします (または Ctrl キーと Shift キーを押しながら F キーを押します)。

 **[すべて検索]** を選択すると、 **[検索結果]** ウィンドウが開き、検索に対する一致項目が一覧表示されます。 一覧内でいずれかの検索結果を選択すると、関連付けられたファイルが表示され、一致項目が強調表示されます。 まだファイルが編集用に開いていなければ、タブ ウェルの右側にあるプレビュー タブで開かれます。 **[検索結果]** ボックスの一覧内の検索にも **[検索]** コントロールを使用できます。

### <a name="creating-custom-search-folder-sets"></a>カスタムの検索フォルダー セットの作成
 **[検索対象]** ボックスの横にある **[検索フォルダーの選択]** ボタン ( **[...]** ) をクリックすると、検索スコープを定義できます。 **[検索フォルダーの選択]** ダイアログ ボックスでは、検索対象としてフォルダーのセットを指定し、その指定内容を後で再利用できるように保存することができます。 リモート コンピューター上のフォルダーは、そのコンピューターのドライブがローカル コンピューターにマッピングされている場合のみ、指定することができます。

### <a name="creating-custom-component-sets"></a>カスタムのコンポーネント セットの作成
 **[検索対象]** ボックスの横にある **[カスタム コンポーネント セットの編集]** をクリックすると、コンポーネント セットを検索スコープとして定義できます。 インストールされている .NET または COM コンポーネント、ソリューションに含まれている Visual Studio プロジェクト、または任意のアセンブリやタイプ ライブラリ (.dll、.tlb、.olb、.exe、.ocx) を指定できます。 参照を検索するには、 **[参照内で検索]** チェック ボックスをオンにします。

## <a name="see-also"></a>参照
 [Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)
