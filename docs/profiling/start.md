---
title: Start | Microsoft Docs
description: VSPerfCmd.exe のオプションである Start オプションを使用して、指定されたプロファイリング方法にプロファイラーを初期化する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b85d0fe9-f67a-4b7c-8d48-7eecf3f2dfe9
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: aea1032f709d2f8cebf105bce14dc081fe3b74da
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98719995"
---
# <a name="start"></a>[開始]
**Start** オプションは、指定されたプロファイリング方法にプロファイラーを初期化する *VSPerfCmd.exe* オプションです。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName [Options]
```

#### <a name="parameters"></a>パラメーター
 `Method` 次のいずれかのキーワードとする必要があります。

- **TRACE** - インストルメンテーション メソッドを指定します。

- **SAMPLE** - サンプリング方法を指定します。

- **COVERAGE** - コード カバレッジを指定します。

- **CONCURRENCY** - リソースの競合メソッドを指定します。

## <a name="required-options"></a>必須オプション
 **Output** オプションは、コマンド ラインで **Start** が指定されている場合に指定する必要があります。

 **出力:** `filename` 出力ファイル名を指定します。

## <a name="exclusive-options"></a>排他的なオプション
 次のオプションは、コマンド ラインで **Start** とともにのみ使用できます。

 **CrossSession**&#124;**CS** プロセス間のプロファイリングを有効にします。 オプション名 **CrossSession** と **CS** は両方ともサポートされています。

 **User:** [`domain\`]`username` 指定されたアカウントからモニターへのクライアント アクセスを有効にします。

 **WinCounter:** `Path` [**Automark**:`n`] **WinCounter** はプロファイリング データ ファイル内にマークとして含める Windows パフォーマンス カウンターを指定します。 **AutoMark** は、データ ファイルのコレクション間の間隔をミリ秒単位で指定します。

## <a name="invalid-options"></a>無効なオプション
 次のオプションは、コマンド ラインで **Start** オプションとともに使用することができません。

 **Status** **Status** は、プロファイリングされるプロセスに適用されます。 プロセスとスレッドが現在のプロファイル状態 (オン/オフ) とともに一覧表示されます。 たとえば、プロセスが停止されても、**Status** はこのプロセスをレポートに記録しません。 **Status** は、プロセスがプロファイリングされているかどうかを示します。

 **Shutdown**[ **:** `Timeout`] プロファイラーをオフにします。

## <a name="example"></a>例
 次の例では、*VSPerfCmd.exe の* **Start** オプションを使用してプロファイラーを初期化する方法を示します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
