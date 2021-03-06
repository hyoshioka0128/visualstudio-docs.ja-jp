---
title: '方法: 非表示のデバッガー コマンドを復元 |Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, restoring commands
- debugging [Visual Studio], restoring commands
- commands, debugger
ms.assetid: 76ac9b77-f536-43b5-a9fc-984854b1c566
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5edc195397b9652d790620b8281100cc7651a02d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802305"
---
# <a name="how-to-restore-hidden-debugger-commands"></a>方法 : 非表示のデバッガー コマンドを復元する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio をセット アップするときに、既定の IDE 設定で主要なプログラム言語を選択するように指示されます。 言語によっては、既定の IDE 設定で一部のデバッガー コマンドが非表示のことがあります。  
  
 既定の IDE 設定で非表示のデバッガー機能を使用するには、次の手順でコマンドをメニューに表示します。  
  
### <a name="to-restore-hidden-debugger-commands"></a>非表示のデバッガー コマンドを復元するには  
  
1.  プロジェクトを開き、[、**ツール**] メニューのをクリックして**カスタマイズ**します。  
  
2.  **カスタマイズ**ダイアログ ボックスで、をクリックして、**コマンド**タブ。  
  
3.  **メニュー バー:** ドロップダウンで、選択、**デバッグ**復元されたコマンドを格納するメニュー。  
  
4.  をクリックして、**コマンドを追加しています.** を追加します。  
  
5.  **コマンドの追加**ボックスで、をクリックし、追加するコマンドを選択**OK**します。  
  
6.  前の手順を繰り返して、ブレークポイントを追加します。  
  
7.  クリックして**閉じる**メニューにコマンドの追加が完了したら。  
  
    > [!WARNING]
    >  メニュー項目によっては、デバッガーが特殊なモード (実行モードまたは中断モード) のときにのみ表示されます。 そのため、この手順でコマンドを追加しても、すぐに表示されないことがあります。  
  
## <a name="restoring-commands-not-available-from-the-customize-dialog-box"></a>[ユーザー設定] ダイアログ ボックスから使用できないコマンドを復元する  
 特に階層メニューに含まれるいくつかのコマンドをから復元することはできません、**カスタマイズ** ダイアログ ボックス。 このようなコマンドを復元するには、IDE 設定の新しいコレクションをインポートする必要があります。  
  
#### <a name="to-import-new-ide-settings"></a>新しい IDE 設定をインポートするには  
  
1.  **ツール** メニューのをクリックして**インポートおよびエクスポート設定**します。  
  
2.  **のインポートとエクスポートの設定ウィザードへようこそ**] ページで [**選択された環境設定をインポート**、順にクリックします**次**。  
  
3.  **現在の設定の保存**ページで、クリックして、既存の設定を保存するかどうかを決定**次**します。  
  
4.  **をインポートする設定のコレクションを選択**ページの**既定の設定**フォルダーを使用するコマンドが含まれる開発設定のコレクションを選択します。 選択するコレクションがわからない場合**汎用開発設定**または**Visual C 開発設定**、これは、ほとんどのデバッガー コマンドを提供します。  
  
5.  **[次へ]** をクリックします。  
  
6.  **をインポートする設定の選択**] ページ [**オプション**、ことを確認します**デバッグ**が選択されています。 この設定をインポートしないのであれば、他のチェック ボックスはオフにします。  
  
7.  **[完了]** をクリックします。  
  
8.  **インポートの完了**設定のリセットに関連付けられているエラーを確認 ページで、**詳細**します。  
  
9. **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [デバッガーの基本事項](../debugger/debugger-basics.md)



