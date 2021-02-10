---
title: DebugBreak と __debugbreak | Microsoft Docs
description: ブレークポイントが設定されている場合と同様に、DebugBreak 関数と __debugbreak の組み込みを使用して、プログラムを中断させる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- DebugBreak
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], DebugBreak function
- DebugBreak function
- breakpoints, DebugBreak function
ms.assetid: 9787c795-df94-4f48-bc8d-3bf899b67421
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f4fb03cf4d45e367f0d7a99dbe26705475652651
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873146"
---
# <a name="debugbreak-and-__debugbreak"></a>DebugBreak と __debugbreak
[DebugBreak](/windows/win32/api/debugapi/nf-debugapi-debugbreak) Win32 関数または [__debugbreak](/cpp/intrinsics/debugbreak) 組み込み関数は、コード内のどこからでも呼び出すことができます。 `DebugBreak` および `__debugbreak` を呼び出した場合の動作は、その位置にブレークポイントを設定した場合と同様です。

 `DebugBreak` はシステム関数の呼び出しであるため、システム デバッグ シンボルをインストールして、中断の後に正しい呼び出し履歴情報が表示されるようにする必要があります。 そうしなかった場合、デバッガーによって表示される呼び出し履歴情報は、1 フレームずれて表示されることがあります。 `__debugbreak` を使用した場合、シンボルは不要です。

## <a name="see-also"></a>関連項目
- [コンパイラの組み込み](/cpp/intrinsics/compiler-intrinsics)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
- [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
