---
title: セキュリティ警告:デバッガーで信頼されないコマンドを実行する必要があります | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.sourceserver.securityalert
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: e5c004b3-b364-4098-ac98-770076ca9981
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a29ba026f9b3c2b8839d474c2d0833eb79f7ffd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683297"
---
# <a name="security-warning-debugger-must-execute-untrusted-command"></a>セキュリティ警告:デバッガーは信頼されないコマンドを実行する必要があります
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ソース サーバーを使用している場合、この警告ダイアログ ボックスが表示されます。 デバッガーがソース コードを取得するために実行する必要のあるコマンドが、srcsvr.ini ファイルに含まれる、ソース サーバーに対して信頼できるコマンドの一覧に記載されていないことを示します。 このコマンドが有効な場合、srcsvr.ini ファイルに追加できます。 それ以外の場合は、そのコマンドを実行しないようにしてください。 詳細については、[シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事をご覧ください。  
  
## <a name="message-text"></a>メッセージ テキスト  
 **ソース サーバーからソースを取得するために、この信頼されていないコマンドを実行します。**  
  
 **既知の信頼できる発信元からのデバッグ シンボル ファイル (\*.pdb) でない場合、コマンドは無効であるか、または実行に危険が伴うおそれがあります。**  
  
 **このコマンドを実行しますか。**  
  
## <a name="uielement-list"></a>UIElement の一覧  
 テキスト ボックス  
 実行する .pdb ファイルからのコマンド。  
  
 実行  
 コマンドの実行を許可します。  
  
 [実行しない]  
 コマンドの実行およびソース サーバーからのファイルのダウンロードを停止します。  
  
## <a name="see-also"></a>参照  
 [シンボル (.pdb) とソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [ソース サーバー](https://msdn.microsoft.com/library/windows/desktop/ms680641\(v=vs.85\).aspx)
