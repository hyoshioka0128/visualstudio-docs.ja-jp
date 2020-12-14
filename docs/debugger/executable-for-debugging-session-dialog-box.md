---
title: '[デバッグ セッションで実行可能] ダイアログ ボックス | Microsoft Docs'
description: DLL をデバッグするには、実行可能ファイルを指定して、DLL を呼び出す必要があります。 実行可能ファイルが指定されていない場合に表示されるダイアログ ボックスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.exefordebug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- executable files, specifying when debugging
- DLLs, debugging
- debugger, Executable for Debugging Session dialog box
- Executable for Debugging Session dialog box
ms.assetid: c0ddbe32-b99f-4425-acf1-f48842804f56
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f4f1f1a88ad30d5102043571473be0d72d71a054
ms.sourcegitcommit: 47da50a74fcd3db66d97cb20accac983bc41912f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96863050"
---
# <a name="executable-for-debugging-session-dialog-box"></a>[デバッグ セッションで実行可能] ダイアログ ボックス

このダイアログ ボックスは、ダイナミック リンク ライブラリ (DLL: Dynamic-Link Library) をデバッグするときに、実行可能ファイルが指定されていない場合に表示されます。 Visual Studio では、DLL を直接起動することはできません。 代わりに、Visual Studio では、特定の実行可能ファイルが起動されます。 DLL のデバッグは、実行可能ファイルから呼び出されたときに実行できます。

 **実行可能ファイル名**: デバッグする DLL を呼び出す実行可能ファイルのパス名を入力します。

 **プロジェクトにアクセスする URL (ATL Server のみ)** : ATL Server の DLL をデバッグする場合は、プロジェクトが存在する URL を入力します。

 入力すると、これらの設定がプロジェクトの [プロパティ ページ] に保存されるため、以降のデバッグ セッションで再入力する必要がなくなります。 設定変更が必要な場合は [プロパティ ページ] を開いて値を変更できます。 デバッグ セッションで実行可能ファイルを指定する方法の詳細については、[DLL のデバッグ](../debugger/how-to-debug-from-a-dll-project.md)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)