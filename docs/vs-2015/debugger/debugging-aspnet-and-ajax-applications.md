---
title: ASP.NET と AJAX アプリケーションのデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, WCF
- debugging ASP.NET Web applications
- debugging [ASP.NET], about ASP.NET debugging
- WCF, debugging
ms.assetid: 9d531913-541b-47b8-864d-138021fca0c6
caps.latest.revision: 34
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e0645cd28e6124e31e19b03489661c6828799cf4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686744"
---
# <a name="debugging-aspnet-and-ajax-applications"></a>ASP.NET アプリケーションおよび AJAX アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web アプリケーションのデバッグ方法は、Windows フォームなど、他の Windows アプリケーションの場合と似ています。どちらのアプリケーションも、コントロールとイベントが関係するためです。 ただし、これらのアプリケーションには基本的な違いもあります。  
  
- 状態の追跡は、Web アプリケーションの方が複雑です。  
  
- Windows アプリケーションでは、ほとんどの場合、デバッグ対象のコードは 1 か所にあります。Web アプリケーションでは、クライアント側とサーバー側の両方に存在することがあります。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] コードはすべてサーバーにありますが、クライアント側に JavaScript や [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コードが存在することがあります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ASP.NET のデバッグの準備](../debugger/preparing-to-debug-aspnet.md)  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションのデバッグを有効にするために必要な手順について説明します。  
  
 [Web アプリケーションのデバッグ](../debugger/debugging-web-applications.md)  
 AJAX 対応のスクリプト アプリケーションなどの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションをデバッグする方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] の例外のデバッグ時に "マイ コードのみ" を有効にする必要がある理由について説明します。  
  
 [Ajax アプリケーションのデバッグとトレースの概要](https://msdn.microsoft.com/library/92684ea0-7bb4-4a34-9203-3aa6394ce375)  
 AJAX コードをデバッグするのに役立つ方法とツールについて説明します。  
  
 [IntelliTrace](../debugger/intellitrace.md)  
 アプリケーションの状態の履歴を記録してレビューする IntelliTrace を使用することで、アプリケーションの頻繁な再起動がなくなり、コードのデバッグ時間を短縮します。 アプリケーションの実行中に発生するイベントや呼び出しに関する情報を確認し、それらのポイントに合わせてデバッグを開始することができます。 Visual Studio Ultimate が必要です。  
  
## <a name="see-also"></a>参照  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [Web アプリケーションとスクリプトのデバッグ](../debugger/debugging-web-applications-and-script.md)   
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [デバッガーの基本事項](../debugger/debugger-basics.md)
