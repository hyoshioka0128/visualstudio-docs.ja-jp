---
title: '[ウィンドウ] タブ ([ウィンドウ プロパティ] ダイアログ ボックス) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Window Properties dialog box, Windows Tab
ms.assetid: 9001342a-09a8-4f5e-b6ed-881a3b9d7246
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c474a85499b221a3ee1d5dfd6befb872f6710f63
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68159693"
---
# <a name="windows-tab-window-properties-dialog-box"></a>[ウィンドウ] タブ ([ウィンドウ プロパティ] ダイアログ ボックス)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

選択したウィンドウに関連するウィンドウに関する情報を表示するには、 **[ウィンドウ]** タブを使用します。 [[ウィンドウ プロパティ] ダイアログ ボックス](../debugger/window-properties-dialog-box.md)を表示するには、[[ウィンドウ ビュー]](../debugger/windows-view.md) ウィンドウにフォーカスを移動します。 ツリーで任意のウィンドウ ノードを選択し、 **[ビュー]** メニューから **[プロパティ]** を選択します。  
  
 **[ウィンドウ]** タブでは、次の設定を使用できます。  
  
|入力|説明|  
|-----------|-----------------|  
|**次のウィンドウ**|ウィンドウ ツリー ビューに表示される同じシーケンス (Z オーダー) 内の次の兄弟ウィンドウのハンドル (次のウィンドウがない場合は "none")。 このエントリは、次のウィンドウのプロパティを表示する場合に選択します。|  
|**前のウィンドウ**|ウィンドウ ツリー ビューに表示される同じシーケンス (Z オーダー) 内の前の兄弟ウィンドウのハンドル (前のウィンドウがない場合は "none")。 このエントリは、前のウィンドウのプロパティを表示する場合に選択します。|  
|**親ウィンドウ**|このウィンドウの親ウィンドウのハンドル (親がない場合は "none")。 このエントリは、親ウィンドウのプロパティを表示する場合に選択します。|  
|**最初の子**|ウィンドウ ツリー ビューに表示されるシーケンス (Z オーダー) 内の、このウィンドウの最初の子ウィンドウのハンドル (子ウィンドウがない場合は "none")。 この値は、最初の子ウィンドウのプロパティを表示する場合に選択します。|  
|**オーナー ウィンドウ**|このウィンドウのオーナー ウィンドウのハンドル。 アプリケーションのメイン ウィンドウは、通常、システムモーダル ダイアログ ウィンドウなどを所有しています (オーナーがない場合は "none")。 このエントリは、オーナー ウィンドウのプロパティを表示する場合に選択します。|
