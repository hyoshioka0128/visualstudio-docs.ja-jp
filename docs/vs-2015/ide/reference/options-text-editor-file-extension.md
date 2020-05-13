---
title: '[オプション]、[テキスト エディター]、[ファイル拡張子] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.toolsoptionspages.text_editor.file_extension
helpviewer_keywords:
- file extensions, associating to editor
- Editing Experience
- Options dialog box
- Editing Experience, selecting
ms.assetid: 05298fc5-fc4e-4bb2-b942-1f7d2dcdff0f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 26c53633bc55efcf95ffbc579e24d2d61e4a0932
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662270"
---
# <a name="options-text-editor-file-extension"></a>[オプション]、[テキスト エディター]、[ファイル拡張子]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

この [オプション] ダイアログでは、Visual Studio 統合開発環境 (IDE) で特定のファイル拡張子を持つすべてのファイルを処理する方法を指定できます。 入力した**拡張子**ごとに、[使用したエディター] を選択できます。 これにより、特定の種類の文書を開く IDE のエディターまたはデザイナーを選択できます。 オプションを表示するには、**[ツール]** メニューから **[オプション]** を選択し、**[テキスト エディター]** ノードを展開し、**[ファイル拡張子]** を選択します。

 "エンコードあり" オプションを選択すると、その種類の文書を開くときにダイアログが表示され、その文書のエンコード スキームを選択できます。 これは、さまざまなプラットフォームで、あるいはさまざまなターゲット言語で使用できるようにプロジェクト文書の各種バージョンを用意している場合に便利です。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="uielement-list"></a>UIElement の一覧
 **拡張機能**IDE で定義する編集エクスペリエンスを持つファイル拡張子を入力します。

 **エディター**このファイル拡張子を持つドキュメントを開く IDE エディターまたはデザイナーを選択します。 "エンコードあり" オプションを選択すると、その種類の文書を開くときにダイアログが表示され、エンコード スキームを選択できます。

 **[追加]** 指定した **[拡張子]** と **[使用したエディター]** が含まれるエントリを拡張子一覧に追加します。

 **削除**選択したエントリを拡張機能の一覧から削除します。

 拡張機能の一覧には、編集操作が指定されているすべての拡張機能が表示されます。

 **拡張子ファイルのマップ先**このオプションは、IDE で拡張子のないファイルを処理する方法を指定する場合に選択します。

 **拡張子ファイルのオプション** **エディター**と同じ一覧を提供します。 ファイル拡張子のない文書を開く IDE のエディターまたはデザイナーを選択します。

## <a name="see-also"></a>関連項目
 [方法 : エディター モードを管理する](../../ide/how-to-manage-editor-modes.md)
