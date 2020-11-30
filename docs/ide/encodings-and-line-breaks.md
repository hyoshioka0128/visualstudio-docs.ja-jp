---
title: エンコーディングと改行文字
description: Visual Studio で改行として解釈される文字と、元のエンコードと改行文字がどのように維持されるかについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 889af1c0fd28224b2f31eb80bbeecad28346cd1c
ms.sourcegitcommit: 66cda27b63c9b55782b1db223a6dbda9f8cabe13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95006641"
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
> **[ファイル]** メニューに **[保存オプションの詳細設定]** が表示されない場合は、追加することができます。 
> 1. **[ツール]** 、 **[カスタマイズ]** の順に選択します。 
> 1. **[コマンド]** タブを選択し、 **[メニュー バー]** ラジオ ボタンを選択して、対応するドロップダウン リストから **[ファイル]** を選択します。 **[コマンドの追加]** ボタンを選択します。 
> 1. **[コマンドの追加]** ダイアログ ボックスの **[カテゴリ]** の下で、 **[ファイル]** を選択してから、 **[コマンド]** 一覧で **[保存オプションの詳細設定]** を選択します。 **[OK]** ボタンを選択します。
> 1. **[上へ移動]** ボタンと **[下へ移動]** ボタンを使用して、コマンドをメニュー内の任意の位置に移動します。 **[閉じる]** を選び、 **[カスタマイズ]** ダイアログ ボックスを閉じます。 
> 詳細については、「[メニューまたはツール バーのカスタマイズ](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#customizing_menu)」を参照してください。
>
> または、 **[ファイル]**  >  **[名前を付けて \<file\> を保存]** を選択して **[保存オプションの詳細設定]** ダイアログ ボックスにアクセスできます。 **[名前を付けてファイルを保存]** ダイアログ ボックスで、 **[保存]** ボタンの横にあるドロップダウンの三角形を選択し、 **[エンコード付きで保存]** を選択します。

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)
