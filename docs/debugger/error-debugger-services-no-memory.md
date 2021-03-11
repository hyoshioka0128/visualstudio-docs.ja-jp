---
description: デバッグ サービスのメモリが不足しているため、デバッグ セッションが終了しました。
title: デバッガー サービスのメモリが不足しています | Microsoft Docs
ms.date: 07/10/2019
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.debug_no_memory
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger
author: isadorasophia
ms.author: isgarcia
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: d881248652d644e9a82725b0d083d095ff72f885
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147043"
---
# <a name="debugger-services-running-out-of-memory"></a>デバッガー サービスのメモリが不足しています
デバッグ サービスのメモリが不足しているため、デバッグ セッションが終了しました。

## <a name="to-investigate-this-error-on-windows"></a>Windows でこのエラーを調査するには
- **[診断ツール]** ウィンドウでプロセス メモリ グラフをチェックして、ターゲット アプリケーションでメモリ使用量が増大しているかどうかを確認できます。 該当する場合は、**メモリ使用量** ツールを使用して根本的な問題を診断し、「[メモリ使用量の分析](../profiling/memory-usage.md)」を参照してください。

- ターゲット アプリケーションで大量のメモリが消費されていると思えない場合は、**タスク マネージャー** ウィンドウを使用して、Visual Studio (devenv.exe)、ワーカー プロセス (msvsmon.exe)、または VS Code (vsdbg.exe/vsdbg-ui.exe) のメモリ使用量をチェックして、これがデバッガーの問題かどうかを判断します。 メモリ不足のプロセスが devenv.exe の場合は、実行中の Visual Studio 拡張機能の数を減らすことを検討してください。

## <a name="see-also"></a>関連項目
- [ブログの投稿:デバッグ中に CPU とメモリを分析する](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)
- [メモリ管理について](/windows/win32/memory/about-memory-management)
