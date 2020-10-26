---
title: エラー :サーバーに自動的にステップ インできません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.causality_no_server_response
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
- remote debugging, notification error
ms.assetid: 9a370ccc-d358-429c-b285-9b6c0649bc68
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8dcb8fa757f1cccf2f3aef6c2520e0c61da0b9f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682675"
---
# <a name="error-unable-to-automatically-step-into-the-server"></a>エラー :サーバーに自動的にステップ インできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーは次のように表示されます。  
  
 サーバーに自動的にステップ インできません。 デバッガーは、リモート プロシージャが実行される前に通知されませんでした。  
  
 このエラーは、Web サービスにステップ インしようとすると発生することがあります (「 [XML Web サービスへのステップ イン](https://msdn.microsoft.com/8e67de38-bf5f-41cc-a457-1b88ce63d764)」を参照してください)。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] が正しくセットアップされていない場合に発生する可能性があります。  
  
 考えられる原因:  
  
- [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションの web.config ファイルでデバッグを "true" に設定していません (「 [方法: .NET アプリケーションのデバッグを有効にする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)」を参照してください)。  
  
- いずれかのバージョンの [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] が Visual Studio のインストール後にインストールされました。 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] は Visual Studio のインストール前にインストールする必要があります。 この問題を解決するには、Windows の **[コントロール パネル]** で **[プログラムと機能]** を使用して、Visual Studio のインストールを修復します。  
  
## <a name="see-also"></a>参照  
 [リモートデバッグエラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Remote Debugging](../debugger/remote-debugging.md)
