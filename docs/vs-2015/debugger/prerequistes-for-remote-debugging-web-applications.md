---
title: Web アプリケーションをリモートデバッグするための前提条件 |Microsoft Docs
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
- debugging ASP.NET Web applications, remote servers
- remote debugging, prerequisites
- remote servers, debugging Web applications
ms.assetid: 1cd777b5-6d20-4ca6-a0df-51653b118469
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8cbf0ae920be00980d270aae16d5e7d1f7a5313
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72574627"
---
# <a name="prerequisites-for-remote-debugging-web-applications"></a>Web アプリケーションをリモート デバッグするための前提条件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーを使用すると、ローカル コンピューターやリモート サーバーで、Web アプリケーションを透過的にデバッグできます。 これは、どちらのコンピューターでもデバッガーの動作は同じであり、同じ機能を使用できることを意味します。 ただし、リモート デバッグを正常に機能させるには、いくつかの必要条件があります。  
  
- デバッグを実行するサーバーに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] リモート デバッグ コンポーネントをインストールする必要があります。 詳細については、「 [リモートデバッグ](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)のセットアップ」を参照してください。  
  
- 既定で、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスは ASPNET ユーザー プロセスとして実行されます。 このため、それをデバッグするには、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] が実行されているコンピューターに対する管理者特権が必要です。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ワーカー プロセスの名前は、デバッグ シナリオや IIS のバージョンによって変わります。 詳細については、[ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ASP.NET と AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [システム要件](../debugger/aspnet-debugging-system-requirements.md)
