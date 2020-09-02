---
title: エラー :ユーザーがストアド プロシージャ sp_enable_sql_debug を実行できませんでした | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.sqlde_accessdenied
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 11957495-c238-4cc5-8937-e4026f5e10e1
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 759386728283d3d39219133e53668afe3259714a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697673"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>エラー :ユーザーがストアド プロシージャ sp_enable_sql_debug を実行できませんでした
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ストアド プロシージャ sp_enable_sql_debug がサーバーで実行できません。 考えられる原因を以下に示します。  
  
- 接続の問題。 サーバーへの接続が安定している必要があります。  
  
- サーバーで必要な権限の不足。 SQL Server 2005 でデバッグするには、Visual Studio を実行するアカウントと SQL Server に接続するために使用するアカウントの両方が sysadmin ロールのメンバーであることが必要です。 SQL Server に接続するために使用するアカウントは、使用している Windows ユーザー アカウント (Windows 認証を使用している場合) またはユーザー ID とパスワードが設定されたアカウント (SQL 認証を使用している場合) です。  
  
  詳細については、「[方法:デバッグ用の SQL Server の権限を設定する](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [方法: デバッグのための SQL Server アクセス許可を設定する](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [SQL デバッグの設定](https://msdn.microsoft.com/3db09e68-edcc-42de-9c22-4e97cfd55ab3)
