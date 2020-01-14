---
title: 'エラー: Transact-sql の実行はデバッグなしで終了しました |Microsoft Docs'
ms.date: 11/08/2018
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- CSharp
- VB
- FSharp
- C++
- SQL
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e86e24f775d8470b54ed7b9c54d27a5d3c1ee8da
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916303"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>Transact-SQL の実行は、デバッグされないで終了しました。

このエラーは、Transact-sql または SQLCLR プロシージャをデバッグしようとしているときに、デバッガーが SQL Server からデバッグメッセージを受信しない場合に発生します。

この問題は、ネットワークの問題や SQL Server の問題のために発生する可能性がありますが、最も可能性の高い原因はアクセス許可の問題です。

このエラーには、次の 2 つのアカウントが関係します。

- アプリケーション アカウントは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を実行しているユーザー アカウントです。

- 接続アカウントは、SQL Server に接続するために使用される ID です。 このアカウントは、接続が SQL 認証を使用している場合と同じように、Visual Studio が実行されている id と同じである必要はありません。

  SQL デバッグでは、アプリケーションアカウントが接続アカウントと一致しているか、sysadmin である必要があります。

  Sa などの SQL アカウント名を使用している場合は、アプリケーションアカウントを sysadmin として SQL Server に設定する必要があります。 既定では、SQL server が実行されているコンピューターの管理者は、SQL Server していません。

  このエラーを解決するには、次の手順を行う必要があります。

  - アクセス許可の設定を確認します。 詳細については、「[方法: デバッグのための SQL Server アクセス許可を設定する](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)」を参照してください。

  - SQL デバッグが正しく設定されていることを確認します。

  - ネットワーク管理者またはデータベース管理者に問い合わせます。

## <a name="see-also"></a>関連項目

- [SQL デバッグの設定](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))
- [方法: デバッグのための SQL Server アクセス許可を設定する](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
- [Remote Debugging](../debugger/remote-debugging.md)