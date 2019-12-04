---
title: Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 79614283-6733-4592-a53a-d428052271ad
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 634169607a7d581de1b1332d78e8d5abde1a722e
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74773740"
---
# <a name="attach"></a>Attach
*VSPerfCmd.exe* **Attach** オプションは、プロセス ID (PID) によって指定された実行プロセスのサンプル プロファイリングを開始します。

 **Attach** オプションを使用するには、Start オプションで **Sample** メソッドを指定する必要があります。

> [!NOTE]
> **Start** オプションを **Crosssession** オプションと共に指定した場合、**VSPerfCmd /Attach** または **VSPerfCmd /Detach** を呼び出すには **Crosssession** も指定する必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Attach:ProcessID [Options]
```

#### <a name="parameters"></a>パラメーター
 `ProcessID` 実行プロセスのプロセス ID (PID)。 実行プロセスの PID は、Windows タスク マネージャーの [プロセス] タブに一覧表示されます。

## <a name="valid-options"></a>有効なオプション
 **Attach** オプションと組み合わせて単一コマンド ラインで指定できる **VSPerfCmd** オプションを以下に示します。

 **Crosssession** ログオン セッション以外のセッションでプロファイリング アプリケーションを有効にします。 **Start** オプションが **Crosssession** オプションと共に指定された場合、必須です。

 **Start:** `Method` コマンド ライン プロファイラー セッションを初期化し、指定されたプロファイル方法を設定します。

 **TargetCLR** プロファイル セッションに複数バージョンの .NET Framework 共通言語ランタイム (CLR) が読み込まれている場合に、プロファイルを行う CLR のバージョンを指定します。 既定では、最初に読み込まれたバージョンがプロファイルされます。

 **GlobalOn GlobalOff** プロファイリングを再開 (**GlobalOn**) または一時停止 (**GlobalOff**) しますが、プロファイル セッションは終了しません。

 **ProcessOn:** `PID` **ProcessOff:** `PID` 指定されたプロセスのプロファイリングを再開 (**ProcessOn**) または一時停止 (**ProcessOff**) します。

## <a name="interval-options"></a>間隔のオプション
 Attach コマンド ラインでは、次のサンプリング間隔オプションのいずれかを指定できます。 既定のサンプリング間隔は、10,000,000 プロセッサ クロック サイクルです。

 **Timer**[ **:** `Cycles`]**PF**[ **:** `Events`]**Sys**[<strong>:</strong>Events]**Counter**[ **:** `Name`,`Reload`,`FriendlyName`] サンプリング間隔の数値と種類を指定します。

- **Timer** - すべての `Cycles` プロセッサ クロック サイクルごとにサンプリングを行います。 `Cycles` が指定されていない場合、10,000,000 サイクルが使用されます。

- **PF** - `Events` のページ フォールトごとにサンプリングを行います。 `Events` が指定されていない場合は、10 ページ フォールトが使用されます。

- **Sys** - オペレーティング システムへの `Events` の呼び出しごとにサンプリングを行います。 `Events` が指定されていない場合は、10 システム呼び出しが使用されます。

- **Counter** - `Name` で指定された CPU パフォーマンス カウンターの `Reload` の数値ごとにサンプリングを行います。 必要に応じて、`FriendlyName` でプロファイラー レポート内の列ヘッダーとして使用する文字列を指定できます。

## <a name="example"></a>例
 この例では、プロセス ID が 12345 のアプリケーションの実行インスタンスにアタッチする方法を示しています。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Attach:12345
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
