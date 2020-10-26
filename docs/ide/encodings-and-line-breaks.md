---
title: エンコーディングと改行文字
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.Encoding
helpviewer_keywords:
- line breaks
- encoding
- Visual Studio, encoding
- editors, line breaks
- line break characters
- Visual Studio, line break characters
ms.assetid: 8f9b3ffc-7b8d-44f4-87cb-dc29105be12d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6448b553c1da9e697bca3860cb8507727c99cc08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75588591"
---
# <a name="encodings-and-line-endings"></a>エンコーディングと行の終わり

Visual Studio では、次の文字が改行として解釈されます。

- CR LF:キャリッジ リターン文字とライン フィード文字 (Unicode 文字では 000D + 000A)

- LF:ライン フィード文字 (Unicode 文字では 000A)

- NEL:次行記号 (Unicode 文字では 0085)

- LS:行区切り記号 (Unicode 文字では 2028)

- PS:段落区切り記号 (Unicode 文字では 2029)

他のアプリケーションからコピーされたテキストでは、元のエンコーディングと改行文字が保持されます。 たとえば、メモ帳からテキストをコピーし、Visual Studio でテキスト ファイルに貼り付けた場合、貼り付けたテキストの設定は、メモ帳で使用していた設定と同じになります。

改行文字が異なるファイルを開くと、一致しない改行文字を正規化するかどうか、また、どの種類の改行を使用するかを確認するダイアログ ボックスが表示される場合があります。

## <a name="advanced-save-options"></a>保存オプションの詳細設定

**[ファイル]** メニューの **[保存オプションの詳細設定]** ダイアログ ボックスを使用して、必要な改行の種類を決定できます。 また、同じ設定でファイルのエンコーディングを変更することもできます。

![[保存オプションの詳細設定] ダイアログ ボックス](media/line_endings.png)

> [!NOTE]
> **[ファイル]** メニューに **[保存オプションの詳細設定]** が表示されない場合は、追加することができます。 **[ツール]** 、 **[カスタマイズ]** の順に選択し、 **[コマンド]** タブを選択します。**メニュー バー**のドロップダウン リストで、 **[ファイル]** を選択し、 **[コマンドの追加]** ボタンを選択します。 **[コマンドの追加]** ダイアログ ボックスの **[カテゴリ]** の下で、 **[ファイル]** を選択してから、 **[コマンド]** 一覧で **[保存オプションの詳細設定]** を選択します。 **[OK]** を選択し、 **[下へ移動]** ボタンを選び、コマンドをメニュー内の任意の場所に移動します。 **[閉じる]** を選び、 **[カスタマイズ]** ダイアログ ボックスを閉じます。 詳細については、「[メニューまたはツール バーのカスタマイズ](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#customizing_menu)」を参照してください。
>
> または、 **[ファイル]**  >  **[名前を付けて \<file\> を保存]** を選択して **[保存オプションの詳細設定]** ダイアログ ボックスにアクセスできます。 **[名前を付けてファイルを保存]** ダイアログ ボックスで、 **[保存]** ボタンの横にあるドロップダウンの三角形を選択し、 **[エンコード付きで保存]** を選択します。

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)
