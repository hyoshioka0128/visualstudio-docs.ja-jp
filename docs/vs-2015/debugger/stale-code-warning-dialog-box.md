---
title: '[古いコードの警告] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.stalecode
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Stale Code Warning dialog box
- code, stale code warning
- warnings, Stale Code Warning dialog box
- Edit and Continue, stale code
ms.assetid: 594b894c-e652-4e13-a980-9909473d5712
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a89738446bf8c08680835ddccb7efa30c2f740f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65694698"
---
# <a name="stale-code-warning-dialog-box"></a>[古いコードの警告] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このダイアログ ボックスは、**エディット コンティニュ**ではすぐに適用されない、ネイティブ コードへの変更を行った場合に表示されます。 結果として、現在のスタック フレーム内の一部のネイティブ コードが最新でない (陳腐化している) 場合があります。 詳細については、「 [方法: 古いコードを操作する](https://msdn.microsoft.com/c7536e95-66a6-44a0-995d-3fe5035250b4)」を参照してください。  
  
 **[次回からこのダイアログ ボックスを表示しない]**  
 このチェック ボックスをオンにすると、以後エディット コンティニュは、このダイアログ ボックスを表示せずにコード変更を適用します。 この警告がまた表示されるようにするには、 **[オプション]** ダイアログ ボックスで、 **[デバッグ]** フォルダーを開き、 **[エディット コンティニュ]** ページをクリックし、 **[古いコードの警告を表示する]** をオンにします。  
  
## <a name="see-also"></a>参照  
 [サポートされているコード変更 (C++)](../debugger/supported-code-changes-cpp.md)   
 [[エディット コンティニュ] ([オプション] ダイアログ ボックス - [デバッグ])](https://msdn.microsoft.com/library/009d225f-ef65-463f-a146-e4c518f86103)
