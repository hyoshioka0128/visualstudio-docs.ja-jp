---
title: エラー :Web サーバーが制限され、DEBUG 動詞をブロックしています | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.webdbg_debug_verb_blocked
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 9c8c4812-17db-484d-9c1b-ffd9e3bfef5a
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b85efc44b39485476154d0f41f3261b2aeb1ea7c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203210"
---
# <a name="error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb"></a>エラー : Web サーバーが制限され、デバッグの有効化に必要な DEBUG 動詞をブロックしています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IIS Lockdown ツールが実行され、URLScan がインストールされてアクティブになっているため、Web アプリケーションまたは XML Web サービスのステップ インに失敗しました。 この条件によって、IIS は DEBUG の動詞を受け取ることができません。  
  
 URLScan は IIS Lockdown ツールと連携して動作するセキュリティ ツールです。これによって IIS Web サイト管理者は、不要な機能をオフにしたり、サーバーが処理する HTTP 要求の種類を制限したりできます。 URLScan では、特定の HTTP 要求を遮断することによって、有害な要求がサーバーに到達して損害を与えることを防止できます。  
  
 アプリケーションが Windows Server 2003 上の IIS 6.0 で実行されている場合、IIS Lockdown ツールを実行する必要はありません。IIS 6.0 は、同じ機能を備えているためです。  
  
### <a name="to-enable-debugging-on-a-web-server-with-urlscan-installed"></a>URLScan がインストールされた Web サーバーでデバッグを有効にするには  
  
1. Urlscan.ini ファイルを探します。 通常は、次のようなディレクトリの下にあります。  
  
     C:\WINNT\System32\Inetsrv\urlscan  
  
2. このファイルのコピーを作成し、**Urlscan.old** という名前を付けます。  
  
3. メモ帳または任意のテキスト エディターを使って、元の Urlscan.ini ファイルを開きます。  
  
4. Urlscan.ini で、[AllowVerbs] セクションを探します。 DEBUG を [AllowVerbs] セクションに追加します。 DEBUG が [AllowVerbs] セクションにある場合は、セミコロン (;) を削除して、動詞のコメント アウトを解除します。  
  
5. [DenyVerbs] セクションを探します。 DEBUG が [DenyVerbs] セクションにある場合は、それを削除します。  
  
6. ファイルを保存します。  
  
7. サーバーまたは IIS を再起動します。  
  
## <a name="see-also"></a>参照  
 [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)   
 [エラー: Web サーバーでは要求されたリソースを見つけられませんでした](../debugger/error-the-web-server-could-not-find-the-requested-resource.md)
