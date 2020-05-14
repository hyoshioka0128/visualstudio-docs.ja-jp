---
title: '[フォルダーを指定して検索] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.findreplace.findinfiles
- vs.findinfiles
helpviewer_keywords:
- objects [Visual Studio], finding
- text searches, replacing text
- objects [Visual Studio], searching for
- Find and Replace window, Find in Files tab
- text searches, Find and Replace window
- documents, searching
- files, searching
- Find in Files tab, Find and Replace window
ms.assetid: 989e0737-46d7-4474-8453-fad52a74669d
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5e21d0880813452e37c9e20afdc98321e4b2e3a6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655902"
---
# <a name="find-in-files"></a>[フォルダーを指定して検索]
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[フォルダーを指定して検索]** では、指定したファイル セットを検索できます。 見つかった一致項目と実行された処理は、 **[結果オプション]** で選択した **[検索結果]** ウィンドウに表示されます。

 **[検索と置換]** ウィンドウに **[フォルダーを指定して検索]** を表示する場合は、次の方法のいずれかを使用できます。

### <a name="to-display-find-in-files"></a>[フォルダーを指定して検索] を表示するには

1. メニュー バーで **[編集]** 、 **[検索と置換]** の順に選択します。

2. **[フォルダーを指定して検索]** を選択します。

   検索操作を取り消すには、Ctrl キーを押しながら Break キーを押します。

> [!NOTE]
> 検索と置換ツールでは、`Hidden` 属性または `System` 属性が設定されているディレクトリは検索されません。

## <a name="find-what"></a>[検索する文字列]
 新しい文字列や式を検索するには、このボックスで指定します。 最近検索した 20 種類の文字列を検索するには、一覧を開き、検索する文字列をクリックします。 検索文字列に 1 つ以上の正規表現を使用する場合は、隣接する **[式ビルダー]** をクリックします。 詳細については、「[Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

## <a name="look-in"></a>[検索対象]
 **[検索対象]** ドロップダウン リストから選択したオプションにより、 **[フォルダーを指定して検索]** で現在アクティブなファイルのみを検索するか、特定のフォルダー内に格納されているすべてのファイルを検索するかが決まります。 検索スコープを一覧から選択するか、 **[参照] ([...])** ボタンをクリックして **[検索フォルダーの選択]** ダイアログ ボックスを表示し、独自のディレクトリ セットを入力します。 **[検索対象]** ボックスにパスを直接入力することもできます。

> [!WARNING]
> **[ソリューション全体]** または **[現在のプロジェクト]** オプションでは、プロジェクトおよびソリューション ファイルは検索されません。 プロジェクト ファイルを検索対象にするには、検索フォルダーを選択します。

> [!NOTE]
> 選択した **[検索対象]** オプションにより、ソース コード管理からチェックアウトしたファイルを検索する場合は、ローカル マシンにダウンロードされたファイルのバージョンのみが検索されることに注意してください。

## <a name="include-subfolders"></a>サブフォルダーを含める
 **[検索対象]** フォルダーのサブフォルダーが検索されるように指定します。

## <a name="find-options"></a>検索オプション
 **[検索オプション]** セクションは、展開または折りたたむことができます。 次のオプションは、オンまたはオフにできます。

 一致するケースを選択すると、検索**結果**の検索で大文字と小文字が区別されます

 単語単位 を選択した場合、**検索結果** ウィンドウは単語全体の一致だけを返します。

 [正規表現を使用する] チェックボックスをオンにした場合は、[**検索**する文字列] ボックスまたは [**置換後**の文字列] ボックスで、特殊な表記を使用して、一致するテキストのパターンを定義できます。 これらの表記の一覧については、「[Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

 [次のファイルの種類を確認してください] この一覧に**は、検索**対象のファイルの種類が表示されます。 このフィールドが空白の場合は、 **[検索対象]** ディレクトリ内のすべてのファイルが検索されます。

 一覧の項目を選択し、特定の種類のファイルを検索する設定済みの検索文字列を入力します。

## <a name="result-options"></a>結果オプション
 **[結果オプション]** セクションは、展開または折りたたむことができます。 次のオプションは、オンまたはオフにできます。

 検索結果 1 ウィンドウを選択すると、現在の検索結果で **検索結果 1** ウィンドウの内容が置き換えられます。 このウィンドウは自動的に開き、検索結果を表示します。 このウィンドウを手動で開くには、 **[表示]** メニューの **[その他のウィンドウ]** を選択し、 **[検索結果 1]** を選択します。

 検索結果 2 ウィンドウを選択すると、現在の検索結果で **検索結果 2** ウィンドウの内容が置き換えられます。 このウィンドウは自動的に開き、検索結果を表示します。 このウィンドウを手動で開くには、 **[表示]** メニューの **[その他のウィンドウ]** を選択し、 **[検索結果 2]** を選択します。

 表示ファイル名には、検索結果を表示するのではなく、検索結果が含まれるファイルの一覧のみが表示されます。

 結果を追加すると、検索結果が前の検索結果に追加されます。

## <a name="see-also"></a>参照
 [検索と置換](../ide/finding-and-replacing-text.md) [(ファイル内のテキストの置換](../ide/replace-in-files.md)) [Visual Studio のコマンド](../ide/reference/visual-studio-commands.md)
