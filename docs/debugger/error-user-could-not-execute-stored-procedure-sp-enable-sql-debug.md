---
title: エラー - ユーザーがストアド プロシージャ sp_enable_sql_debug を実行できませんでした | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 84326c5c1beb91269a5f097c8c5d7cb8782a7a56
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600154"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>エラー :ユーザーがストアド プロシージャ sp_enable_sql_debug を実行できませんでした

ストアド プロシージャ sp_enable_sql_debug がサーバーで実行できません。 考えられる原因を以下に示します。

- 接続の問題。 サーバーへの接続が安定している必要があります。

- サーバーで必要な権限の不足。 SQL Server 2005 でデバッグするには、Visual Studio を実行するアカウントと SQL Server に接続するために使用するアカウントの両方が sysadmin ロールのメンバーであることが必要です。 SQL Server に接続するために使用するアカウントは、使用している Windows ユーザー アカウント (Windows 認証を使用している場合) またはユーザー ID とパスワードが設定されたアカウント (SQL 認証を使用している場合) です。

詳細については、「[方法:デバッグ用の SQL Server の権限を設定する](/previous-versions/w1bhybwz(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: デバッグ用の SQL Server の権限を設定する](/previous-versions/w1bhybwz(v=vs.100))
- [SQL デバッグの設定](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))