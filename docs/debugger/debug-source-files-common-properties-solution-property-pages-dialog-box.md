---
title: '[デバッグ ソース ファイル] ([ソリューション プロパティ ページ])'
description: Visual Studio で、ソリューション エクスプローラーでソリューションを右クリックし、[プロパティ]、[共通プロパティ] の順に選択し、[デバッグ ソース ファイル] プロパティ ページにアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.options.FindSource
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Debug Source Files property page
- debugging [Visual Studio], specifying source and symbol files
- source files, specifying in debugger
- debugger, source files
ms.assetid: 0af11464-eeb1-4d0b-87a6-0cc96779afb1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 10818f473dec392364832cdc2f5215197ef4627f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873172"
---
# <a name="debug-source-files-common-properties-solution-property-pages-dialog-box"></a>[デバッグ ソース ファイル] ([ソリューション プロパティ ページ] ダイアログ ボックス - [共通プロパティ])
このプロパティ ページでは、ソリューションのデバッグ時にデバッガーによってソース ファイルが検索される場所を指定します。

 **[デバッグのソース ファイル]** プロパティ ページを開くには、**ソリューション エクスプローラー** でソリューションを右クリックし、ショートカット メニューの **[プロパティ]** をクリックします。 **[共通プロパティ]** フォルダーを展開し、 **[デバッグのソース ファイル]** ページをクリックします。

 **[ソース コードを含んでいるディレクトリ]** ソリューションのデバッグ時に、デバッガーでソース ファイルが検索されるディレクトリの一覧が表示されます。 指定されたディレクトリのサブディレクトリも検索されます。

 **[以下のソース ファイルを探さない]** デバッガーで読み取る必要のないファイルの名前を入力します。 デバッガーは、上で指定したディレクトリのいずれかでこれらのファイルを見つけた場合、それを無視します。 デバッグ中に **[ソース ファイルの検索]** ダイアログ ボックスが表示されたときに **[キャンセル]** をクリックすると、検索中のファイルがこのリストに追加され、そのファイルの検索が中止されます。

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)