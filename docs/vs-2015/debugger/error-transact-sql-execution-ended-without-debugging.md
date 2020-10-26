---
title: エラー :Transact-SQL の実行は、デバッグされないで終了しました | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- FSharp
- VB
- CSharp
- C++
- SQL
ms.assetid: 7a4d4999-3973-4339-ba6a-f0d19bcb1d4a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cdfcaa42c55f87711b0889c6a67d1a4799b84fed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681073"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>エラー :Transact-SQL の実行は、デバッグされないで終了しました
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラーは、Transact-SQL プロシージャまたは SQLCLR プロシージャをデバッグしようとしたときに、デバッガーが SQL Server からデバッグ メッセージを受信しなかった場合に発生します。  
  
 このエラーは、ネットワークの問題や SQL Server の問題によって発生することもありますが、最も可能性が高いのはアクセス許可の問題です。  
  
 このエラーには、次の 2 つのアカウントが関係します。  
  
- アプリケーション アカウントは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を実行しているユーザー アカウントです。  
  
- 接続アカウントは、SQL Server に接続するために使用される ID です。 接続が SQL 認証を使用している場合、この ID は Visual Studio が実行されている ID と同じであるとは限りません。  
  
  SQL デバッグでは、アプリケーション アカウントが接続アカウントと一致しているか、または sysadmin である必要があります。  
  
  sa などの SQL ログインを使用している場合は、アプリケーション アカウントが sysadmin として SQL Server 上でセットアップされている必要があります。 既定では、SQL サーバーが実行されているコンピューターの管理者は SQL Server の sysadmin です。  
  
  このエラーを解決するには、次の手順を行う必要があります。  
  
- アクセス許可の設定を確認します。 詳細については、「[方法:デバッグ用の SQL Server の権限の設定](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)に関するページを参照してください。  
  
- SQL デバッグが正しく設定されていることを確認します。  
  
- ネットワーク管理者またはデータベース管理者に問い合わせます。  
  
## <a name="see-also"></a>参照  
 [SQL デバッグの設定](https://msdn.microsoft.com/3db09e68-edcc-42de-9c22-4e97cfd55ab3)   
 [方法: デバッグのための SQL Server アクセス許可を設定する](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)   
 [Remote Debugging](../debugger/remote-debugging.md)
