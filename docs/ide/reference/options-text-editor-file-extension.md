---
title: '[オプション]、[テキスト エディター]、[ファイル拡張子]'
description: '[ファイル拡張子] ページを使用して、特定のファイル拡張子を持つすべてのファイルが Visual Studio IDE によってどのように処理されるかを指定する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.File_Extension
helpviewer_keywords:
- file extensions, associating to editor
- Editing Experience
- Options dialog box
- Editing Experience, selecting
ms.assetid: 05298fc5-fc4e-4bb2-b942-1f7d2dcdff0f
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1d0e782b0d141666ca7d1f79464d60afd89ef871
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96039732"
---
# <a name="options-text-editor-file-extension"></a>[オプション]、[テキスト エディター]、[ファイル拡張子]

この [オプション] ダイアログでは、Visual Studio 統合開発環境 (IDE) で特定のファイル拡張子を持つすべてのファイルを処理する方法を指定できます。 入力した **拡張子** ごとに、[使用したエディター] を選択できます。 これにより、特定の種類の文書を開く IDE のエディターまたはデザイナーを選択できます。 オプションを表示するには、**[ツール]** メニューから **[オプション]** を選択し、**[テキスト エディター]** ノードを展開し、**[ファイル拡張子]** を選択します。

"エンコードあり" オプションを選択すると、その種類の文書を開くときにダイアログが表示され、その文書のエンコード スキームを選択できます。 これは、さまざまなプラットフォームで、あるいはさまざまなターゲット言語で使用できるようにプロジェクト文書の各種バージョンを用意している場合に便利です。

## <a name="uielement-list"></a>UIElement の一覧

**拡張子**

IDE の [使用したエディター] を定義するファイル拡張子を入力します。

**[エディター]**

このファイル拡張子を持つ文書を開く IDE のエディターまたはデザイナーを選択します。 "エンコードあり" オプションを選択すると、その種類の文書を開くときにダイアログが表示され、エンコード スキームを選択できます。

**[追加]**

指定した **[拡張子]** と **[使用したエディター]** が含まれるエントリを拡張子一覧に追加します。

**削除**

拡張子一覧から選択したエントリを削除します。

**[拡張子一覧]**

[使用したエディター] が指定されているすべての拡張子を一覧表示します。

**[拡張子のないファイルの割り当て先]**

拡張子のないファイルを IDE で処理する方法を指定する場合、このオプションを選択します。

**[拡張子のないファイルのオプション]**

**[エディター]** と同じ一覧を提供します。 ファイル拡張子のない文書を開く IDE のエディターまたはデザイナーを選択します。

## <a name="see-also"></a>関連項目

- [方法: エディター モードを管理する](../../ide/how-to-manage-editor-modes.md)
