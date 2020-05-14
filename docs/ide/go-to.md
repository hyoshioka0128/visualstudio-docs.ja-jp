---
title: ファイルへ移動、シンボルへ移動、指定行へのジャンプ
ms.date: 08/14/2018
ms.topic: conceptual
helpviewer_keywords:
- code editor, go to
- code editor, go to line
- go to line
- go to
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb39f1d395e48351aeacb587556224b0f86aac3e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75593786"
---
# <a name="find-code-using-go-to-commands"></a>移動コマンドを使用したコードの検索

Visual Studio の **[移動]** コマンドは、特定の項目をすばやく検索できるように、コードのフォーカス検索を行います。 統一されたシンプルなインターフェイスで、特定の行、型、シンボル、ファイル、メンバーに移動できます。

## <a name="how-to-use-it"></a>使用方法

入力 | 関数
------------ | ---
**キーボード** | **Ctrl**+**T** キーまたは **Ctrl**+ **,** キーを押します。
**マウス** | **[編集]** 、 **[移動]** 、 **[すべてに移動]** の順に選択します。

コード エディターの右上に小さいウィンドウが表示されます。

![[すべてにジャンプ] ウィンドウ](media/go-to-all.png)

テキスト ボックスに入力すると、テキスト ボックスの下のドロップダウン リストに結果が表示されます。 要素に移動するには、一覧の要素を選択します。

![[移動] ウィンドウ](../ide/media/vside_navigatetowindow.png)

疑問符 ( **?** ) を入力して詳しいヘルプ情報を表示することもできます。

![[すべてにジャンプ] のヘルプ](media/go-to-all-help.png)

## <a name="filtered-searches"></a>フィルター処理された検索

既定では、指定した項目がソリューションのすべての項目から検索されます。 ただし、検索語句の前に特定の文字を付けることで、コード検索の対象を特定の種類の要素に限定できます。 **[移動]** ダイアログ ボックスのツール バーでボタンを選択して、簡単に検索フィルターを変更することもできます。 タイプ フィルターを変更するボタンが左側にあり、検索の範囲を変更するボタンが右側にあります。

![メンバーに移動する](../ide/media/vside_navigation_toolbar.png)

### <a name="filter-to-a-specific-type-of-code-element"></a>フィルター処理して特定の種類のコード要素に絞り込む

特定の種類のコード要素に検索を絞り込むには、[検索] ボックスでプレフィックスを指定するか、次の 5 つのフィルター アイコンのいずれかを選択します。

プレフィックス | アイコン | ショートカット | 説明
:-: | - | - | -
:| ![行アイコン](media/gotoall-line-icon.png) | **Ctrl**+**G** | 指定した行番号に移動します。
f| ![ファイル アイコン](media/gotoall-files-icon.png) | **Ctrl**+**1**、**Ctrl**+**F** | 指定したファイルに移動します。
r| ![最近使ったファイル アイコン](media/gotoall-recent-files-icon.png) | **Ctrl**+**1**、**Ctrl**+**R** | 指定した、最近アクセスしたファイルに移動します
t| ![型アイコン](media/gotoall-types-icon.png) | **Ctrl**+**1**、**Ctrl**+**T** | 指定した型に移動します。
m| ![メンバー アイコン](media/gotoall-members-icon.png) | **Ctrl**+**1**、**Ctrl**+**M** | 指定したメンバーに移動します。
\#| ![シンボル アイコン](media/gotoall-symbols-icon.png) | **Ctrl**+**1**、**Ctrl**+**S** | 指定したシンボルに移動します。

### <a name="filter-to-a-specific-location"></a>フィルター処理して特定の場所に絞り込む

特定の場所に検索を絞り込むには、次の 2 つのドキュメント アイコンのいずれかを選択します。

アイコン | 説明
---- | ---
![現在のドキュメント](media/gotoall_currentdocument.png) | 現在のドキュメントだけを検索します
![外部ドキュメント](media/gotoall_external.png) | プロジェクト/ソリューションに含まれるドキュメントだけでなく外部のドキュメントも検索します

## <a name="camel-casing"></a>camel 規約に従った大文字小文字の使い分け

コード内で [camel 規約に従った大文字小文字の使い分け](https://en.wikipedia.org/wiki/Camel_case)を使用している場合は、コード要素名の大文字のみを入力することにより、コードの検索が速くなります。 たとえばコードで `CredentialViewModel` という型を使用している場合は、[移動] ダイアログ ボックスで**型**フィルター (**t**) を選択し、名前に含まれる大文字 (`CVM`) だけを入力します。 この機能は、コード中に長い名前がある場合に便利です。

![[移動] ウィンドウ - 大文字を使用した検索](../ide/media/vside_capitalsearch.png)

## <a name="settings"></a>設定

歯車アイコンを選択すると、 ![歯車アイコン](media/gotoall_gear.png) この機能の動作を変更することができます。

設定 | 説明
------- | ---
プレビュー タブを使用する | 選んだ項目を IDE の [プレビュー] タブにすぐに表示します
詳細の表示 | プロジェクト、ファイル、行、およびドキュメントのコメントから取得した概要情報をウィンドウに表示します。
ウィンドウを中央に | このウィンドウをコード エディターの右上ではなく、中央に移動します。

## <a name="see-also"></a>関連項目

- [コード間の移動](../ide/navigating-code.md)
- [[指定行へのジャンプ] ダイアログ ボックス](../ide/reference/go-to-line.md)
- [[定義へ移動] と [定義をここに表示]](../ide/go-to-and-peek-definition.md)
