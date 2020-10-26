---
title: 'ASP.NET のデバッグ: システム要件 | Microsoft Docs'
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
- debugging ASP.NET Web applications, system requirements
- debugging ASP.NET Web applications, security requirements
ms.assetid: 7810b9b2-debf-4271-8fc7-1df031123255
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: aa8951be6da4d77ffb51b6bc8f09a796b373a944
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67826256"
---
# <a name="aspnet-debugging-system-requirements"></a>ASP.NET のデバッグ: システム要件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] のデバッグ シナリオに必要なソフトウェアとセキュリティの要件について説明します。  
  
- ローカル デバッグ。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] と Web アプリケーションが同じコンピューターで実行されている場合のデバッグです。 このシナリオには、2 つのバージョンがあります。  
  
  - [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] コードがファイル システムに存在する場合  

  - [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] コードが IIS の Web サイトに存在する場合  
  
- リモート デバッグ。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] はクライアント コンピューターで実行され、リモート サーバー コンピューターで実行されている Web アプリケーションをデバッグします。  
  
## <a name="security-requirements"></a>セキュリティ要件  
 リモート デバッグでは、ローカル コンピューターとリモート コンピューターが同じドメイン内または同じワークグループ内にセットアップされている必要があります。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスをデバッグするには、そのプロセスをデバッグするアクセス許可が必要です。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションは、既定では **ASPNET** ユーザーとして実行されます。 ワーカー プロセスが **ASPNET**(既定) または **NETWORK SERVICE**として実行されている場合、そのプロセスをデバッグするには管理者特権が必要です。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスの名前は、デバッグ シナリオや IIS のバージョンによって異なります。 詳細については、[ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)」を参照してください。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスを実行しているユーザー アカウントは、IIS を実行しているサーバーの machine.config ファイルを編集することによって変更できます。 これを行うには、 **インターネット インフォメーション サービス (IIS) マネージャー**を使用するのが最善です。 詳細については、[ユーザー アカウントでワーカー プロセスを実行する](../debugger/how-to-run-the-worker-process-under-a-user-account.md)」を参照してください。  
  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスを自分のユーザー アカウントで実行するように変更する場合、IIS を実行しているサーバーの管理者である必要はありません。  
  
> [!CAUTION]
> [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスを別のアカウントで実行するように変更する場合は、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスがそのアカウントで実行中にハックされた場合の影響を考慮する必要があります。 ASPNET および NETWORK SERVICE の各ユーザー アカウントは最小限のアクセス許可で実行されるので、プロセスがハックされた場合の損害が少なくなります。 高い権限のアクセス許可を持つアカウントで [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスを実行する必要がある場合、損害が大きくなる可能性があります。  
  
## <a name="see-also"></a>参照  
 [ASP.NET と AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [方法: ユーザー アカウントでワーカー プロセスを実行する](../debugger/how-to-run-the-worker-process-under-a-user-account.md)
