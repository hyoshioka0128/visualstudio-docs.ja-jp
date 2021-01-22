---
title: '[あいまいさの解決] ダイアログ ボックス | Microsoft Docs'
description: Visual Studio の [あいまいさの解決] ダイアログ ボックスについて確認します。これは、表示する場所をデバッガーで選択できないときに表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.Disambig
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c6f7156a43bc8c5c60415680b4380600e9e695cc
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205607"
---
# <a name="resolve-ambiguity-dialog-box"></a>[あいまいさの解決] ダイアログ ボックス
[`Resolve Ambiguity`] ダイアログ ボックスが表示されるのは、表示する場所をデバッガーが選択できない場合です。 たとえば、C++ テンプレートを使用する場合は、単一の関数テンプレートから複数の関数を作成できます。 デバッガーがテンプレートのソースの場所で停止して、`Go To Disassembly` が選択されている場合、デバッガーには複数のオプションがあります。 テンプレートから作成された各関数は独自の逆アセンブリ コードを持っており、デバッガーはどのコードを表示するのかを認識していません。 [`Resolve Ambiguity`] ダイアログ ボックスでは、対応するすべての場所の一覧から目的の場所を選択できます。

 `Choose the specific location` コマンドに対応するすべての場所の一覧を表示します。

 `Address` 各関数のメモリ アドレスを表示します。

 `Function` 各関数の名前を表示します。

 `Module` 関数のオブジェクト コードを含むモジュール (EXE または DLL) を表示します。

## <a name="see-also"></a>関連項目
- [デバッガー内の式](../debugger/expressions-in-the-debugger.md)