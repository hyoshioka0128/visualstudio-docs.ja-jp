---
title: Mark | Microsoft Docs
description: VSPerfCmd.exe Mark オプションによってプロファイル データ ファイルに指定の情報が挿入されるしくみについて学習します。
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 1d72cef3-bb09-4bbb-8864-6ea0ab623ff9
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 4554a994fe790d5e0ec46762e830576181b312dd
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98722140"
---
# <a name="mark"></a>Mark
*VSPerfCmd.exe の* **Mark** オプションは、プロファイル データ ファイルに指定した情報を挿入します。 マークは個別の VSPerfReport レポートまたはプロファイラー UI のマーク レポート ビューに一覧表示できます。 **Mark** を使用して、レポートおよびビュー フィルターの開始点と終了点を指定できます。

 コマンド ラインで指定するオプションは **Mark** オプションのみにする必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Mark:MarkID,[MarkName]
```

#### <a name="parameters"></a>パラメーター
 `MarkID` プロファイラー ビューおよびレポートにマーク ID として一覧表示される、ユーザー定義の整数。 `MarkID` は一意である必要はありません。

 `MarkName` (省略可能) プロファイラー ビューおよびレポートにマーク名として一覧表示される、ユーザー定義の文字列。 `MarkName` が指定されていない場合、マーク一覧のマーク名フィールドは空になります。 スペースやスラッシュ ("/") を含む文字列は引用符で囲みます。

## <a name="example"></a>例
 この例では、ID が 123 でマーク名が "TestMark" というマークを挿入します。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe
VSPerfCmd.exe /Mark:123,TestMark
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
