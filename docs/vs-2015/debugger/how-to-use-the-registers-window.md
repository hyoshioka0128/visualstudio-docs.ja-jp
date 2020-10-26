---
title: '方法: [レジスタ] ウィンドウを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.registers
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
- registers, debugging
- register contents
- flags, Registers window
- register groups
- debugging [Visual Studio], Registers window
- Registers window
ms.assetid: 2918ffa2-562f-40d6-9053-ef321bbeb767
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 233092af638824c462a6d9a47865a1c6f5fd9397
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697463"
---
# <a name="how-to-use-the-registers-window"></a>方法: [レジスタ] ウィンドウを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[レジスタ] ウィンドウは、 **[オプション]** ダイアログ ボックスにある **[デバッグ]** ノードの **[全般]** カテゴリで、アドレスレベルのデバッグが有効な場合にのみ、使用できます。  
  
 [ **レジスタ** ] ウィンドウには、レジスタの内容が表示されます。 プログラムのステップ実行時に [ **レジスタ** ] ウィンドウを開いたままにしておくと、コードの実行に応じてレジスタ値の変更を確認できます。 最近変更した値が赤で表示されます。 レジスタの値は編集できます。 詳細については、「 [方法: レジスタ値を編集](../debugger/how-to-edit-a-register-value.md)する」を参照してください。  
  
 **[レジスタ]** ウィンドウでは、見やすいようにレジスタがグループ別に整理されますが、グループはプラットフォームやプロセッサの種類によって異なります。 必要に応じて、グループの表示/非表示を切り替えることができます。 詳細については、「 [方法: レジスタグループを表示および非表示にする](../debugger/how-to-display-and-hide-register-groups.md)」を参照してください。  
  
 レジスタとレジスタウィンドウの背後にある概念の概要については、「 [デバッグの基本: レジスタウィンドウ](../debugger/debugging-basics-registers-window.md)」を参照してください。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
### <a name="to-display-the-registers-window"></a>[レジスタ] ウィンドウを表示するには  
  
- [ **デバッグ** ] メニューの [ **ウィンドウ**] をポイントし、[ **レジスタ**] をクリックします。  
  
     デバッガーは動作中であるか、中断モードである必要があります。  
  
    > [!NOTE]
    > スクリプトまたは SQL アプリケーションのレジスタ情報は表示できません。  
  
## <a name="see-also"></a>参照  
 [デバッグの基礎: レジスタウィンドウ](../debugger/debugging-basics-registers-window.md)   
 [デバッガーでのデータの表示](../debugger/viewing-data-in-the-debugger.md)   
 [デバッグの基礎: レジスタウィンドウ](../debugger/debugging-basics-registers-window.md)
