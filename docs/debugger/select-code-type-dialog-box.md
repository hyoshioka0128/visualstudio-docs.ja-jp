---
title: '[コードの種類の選択] ダイアログ ボックス | Microsoft Docs'
description: Visual Studio の [コードの種類の選択] ダイアログ ボックスについて説明します。 このダイアログ ボックスを開くには、[プロセスにアタッチ] ダイアログ ボックスを開き、[選択] をクリックします。
ms.custom: SEO-VS-2020
ms.date: 06/12/2020
ms.topic: reference
f1_keywords:
- vs.debug.selectengines
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- debugging [Visual Studio], engine selection
- debugger, engine selection
- debugging engine selection dialog box
no-loc:
- Blazor WebAssembly
ms.assetid: 932269fe-94e3-43cb-8931-078f31afd177
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7fb7b7625e8e08e291f4f27606d03f9066828e0a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903495"
---
# <a name="select-code-type-dialog-box"></a>[コードの種類の選択] ダイアログ ボックス

このダイアログ ボックスを開くには、 **[プロセスにアタッチ]** ダイアログ ボックスを開き、 **[選択]** をクリックします。

**デバッグするコードの種類を自動的に判断する**: 実行中のコードの種類に基づいて、適切なデバッガーが選択されます。

**次のコードの種類をデバッグする:** 表示される一覧から、デバッグするコードの種類を選択します。 これは、[アタッチの失敗をトラブルシューティング](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md#BKMK_Troubleshoot_attach_errors)するときに役立ちます。 このオプションを使用すると、デバッグするコードの種類のみに検出を制限できます。

::: moniker range=">=vs-2019"
- Blazor WebAssembly - クライアント側 Blazor WebAssembly
- GPU - ソフトウェア エミュレーター - GPU ソフトウェア エミュレーター上で実行される C++ コード
- JavaScript (Chrome) - Chrome で実行される JavaScript
- JavaScript (Microsoft Edge - Chromium) - Windows 10 用 Chromium ベース Microsoft Edge で実行される JavaScript
- JavaScript CDP (V3) デバッガー - CDP クライアントでのデバッグに使用される Chrome DevTools Protocol バージョン 3
- マネージド (CoreCLR) - .NET Core
- マネージド (ネイティブ コンパイル) - C++/CLR コード
- マネージド (v3.5、v3.0、v2.0) - .NET Framework 2.0 以降 (最大 3.5) の .NET Framework コード
- マネージド (v.4.6、v4.5、v4.0) - .NET Framework 4.0 以降の .NET Framework コード
- ネイティブ - C/C++
- Node.js のデバッグ - Node.js ランタイムによってホストされるコード
- Python - Python 
- スクリプト - JavaScript の一般的なスクリプト デバッガーを指定します。 JavaScript (Chrome) など、お客様のシナリオに該当するものがあれば、より制限の厳しいオプションを使用してください。
- T-SQL - Transact-SQL
- Unity - Unity
- マネージド互換モード - マネージド コード用のレガシ デバッガーを指定します。通常、C++/CLR コードを使用した混合モード デバッグで使用するか (混合モードの場合はエディット コンティニュを有効にする)、レガシ デバッガーを対象とした拡張機能をサポートします。 ほとんどの混合モードのデバッグ シナリオでは、マネージド互換モードではなく、 **[ネイティブ]** と適切な **[マネージド]** コードの種類を選択します。
::: moniker-end

ほとんどのシナリオでは、同じデバッグ セッションに複数のデバッガーをアタッチすることはサポートされていません。 これを行うには、Visual Studio の 2 つ目のインスタンスを使用します。

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
