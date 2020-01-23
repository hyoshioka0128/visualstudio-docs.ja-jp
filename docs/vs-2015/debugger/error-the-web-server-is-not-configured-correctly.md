---
title: 'エラー: web サーバーが正しく構成されていません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.remote.projnotconfigured
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 875ba87f-c372-4126-8fe3-e33931cf26c0
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3cfbcf127b9951ddfce1d3db8fe1177087b0350a
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918496"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>エラー : Web サーバーは正しく構成されていません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーでは以下の原因が考えられます。  
  
- デバッグしようとした .NET Web アプリケーションは、別のコンピューターにコピーされたか、手動で名前が変更されたか、または別の場所に移動されています。  
  
- インターネット インフォメーション サービス (IIS) の接続が確立していません IIS への Web サイトの配置に関する詳細については、「 [Web サイトの作成](/iis/get-started/getting-started-with-iis/create-a-web-site)」を参照してください。  
  
- ASP.NET アプリケーションをデバッグしようとしている場合、IIS 8 以降を実行しているリモート コンピューターに配置する手順については、「 [IIS への発行](https://docs.asp.net/en/latest/publishing/iis.html) 」を参照してください。また、IIS 7.5 を実行しているリモート コンピューターに配置する手順については、「 [Remote Debugging ASP.NET on a Remote IIS 7.5 Computer](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Web アプリケーションのデバッグ : エラーおよびトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
