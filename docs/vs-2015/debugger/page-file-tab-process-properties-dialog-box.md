---
title: '[ページ ファイル] タブ ([プロセス プロパティ] ダイアログ ボックス) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: daf41a06-8a55-48f6-95f5-49a8416bd308
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 24fdba37be2373623d94f03e45dc5e8a41a74b84
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192723"
---
# <a name="page-file-tab-process-properties-dialog-box"></a>[ページ ファイル] タブ ([プロセス プロパティ] ダイアログ ボックス)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[ページ ファイル]** タブを使用し、プロセスのページング ファイルを調べます。 [[プロセス プロパティ]](../debugger/process-properties-dialog-box.md) ダイアログ ボックスを表示するには、[[プロセス ビュー]](../debugger/processes-view.md) ウィンドウにフォーカスを移動します。 ツリーで任意のプロセス ノードを選択し、 **[ビュー]** メニューから **[プロパティ]** を選択します。  
  
 **[ページ ファイル]** タブでは、次の設定を使用できます。  
  
|入力|説明|  
|-----------|-----------------|  
|**ページ ファイル サイズ**|ページング ファイルでこのプロセスが使用しているページの現行数。 ページング ファイルには、プロセスによって使用されているデータのページが格納されますが、他のファイルに含まれているデータのページは格納されません。 ページング ファイルはすべてのプロセスで使用されます。ページング ファイルに領域がないと、他のプロセスの実行中、エラーが発生することがあります。|  
|**ピーク ページ ファイルのサイズ**|ページング ファイルでこのプロセスが使用しているページの最大数。|  
|**ページ フォールト**|このプロセスで実行されているスレッド別のページ フォールト数。 ページ フォールトは、スレッドが参照する仮想メモリのページがメイン メモリのワーキング セットにないときに発生します。 したがって、ページがスタンバイ リストにある場合、そのために、既にメイン メモリ内にある場合、またはページを共有している別のプロセスによってページが使用されている場合は、そのページがディスクから取得されません。|
