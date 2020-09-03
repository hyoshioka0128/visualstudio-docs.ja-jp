---
title: '[自動バックアップ] ([オプション] ダイアログ ボックス - [環境]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPag.Environment.AutoRecover
- VS.DialogAutoRestore
- VS.ToolsOptionsPages.Environment.AutoRecover
- VS.ToolsOptionsPages.Environment.Auto_Save_and_Restore
helpviewer_keywords:
- files, recovering
- AutoRecover page
- saving files, automatically
- files, saving automatically
ms.assetid: 397e5e44-4bbe-4289-94d1-642b466c9111
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 743543e03806a842eabc2bbfc69011d63b1264d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72660977"
---
# <a name="autorecover-environment-options-dialog-box"></a>[自動バックアップ] ([オプション] ダイアログ ボックス - [環境])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[オプション] ダイアログ ボックスのこのページを使用し、ファイルを自動的にバックアップするかどうかを指定します。 このページではまた、IDE (統合開発環境) が突然シャットダウンしたとき、変更済みのファイルを復元するかどうかも指定できます。 このダイアログ ボックスにアクセスするには、**[ツール]** メニューを選択し、**[オプション]** を選択し、**[環境]** フォルダーを選択し、**[自動バックアップ]** ページを選択します。 このページが一覧に表示されない場合は、**[オプション]** ダイアログ ボックスの **[すべての設定を表示]** を選択します。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 [**自動回復情報を 1 \<n> 分ごとに保存**する] このオプションを使用して、ファイルがエディターに自動的に保存される頻度をカスタマイズします。 以前に保存されたファイルの場合、ファイルのコピーは \\ . ..\My Documents\Visual Studio \<*version*> \Backup files \\ < *projectname*> に保存されます。 ファイルが新しく、手動で保存されていない場合、ファイルはランダムに生成されたファイル名で自動保存されます。

 [ ** \<n> 日単位の自動回復情報を保持**する] Visual Studio が自動回復用に作成したファイルを保持する期間を指定するには、このオプションを使用します。

## <a name="see-also"></a>参照
 [[オプション] ダイアログボックス](../../ide/reference/options-dialog-box-visual-studio.md)
