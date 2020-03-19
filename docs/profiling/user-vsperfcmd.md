---
title: User (VSPerfCmd) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ee1a478e-374d-4f30-ae28-d260b9d4723a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 7dbb1a155e8e0ffd2690b5850299b8075a63ea3d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779962"
---
# <a name="user-vsperfcmd"></a>User (VSPerfCmd)
**User** オプションは、プロファイリングされるプロセスを所有するアカウントのドメインとユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの **[プロセス]** タブの [ユーザー名] 列に表示されます。

 **User** オプションは、**Start** オプションも含むコマンド ラインでのみ指定できます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName /User:[Domain\]UserName [Options]
```

#### <a name="parameters"></a>パラメーター
 `Domain` ユーザーのドメインの名前。

 `UserName` ユーザーの名前。

## <a name="required-options"></a>必須オプション
 **User** オプションは、**Start** オプションと共に指定する場合にのみ使用できます。

 **Start:** `Method` 指定したプロファイル方法にプロファイラーを初期化します。

## <a name="example"></a>例
 **User** オプションの使用例を以下に示します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /User:SYSTEM
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
