---
title: ネイティブ ランタイム チェックを使用する | Microsoft Docs
description: Visual Studio でネイティブ ランタイム チェックを使用して、スタック ポインターの破損、ローカル配列のオーバーラン、スタックの破損などの一般的なランタイム エラーをキャッチします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- /RTC compiler option [C++], /O compiler option
- run-time checks, native
- stack, pointer corruption
- stack pointers, corruption
- /O compiler option, /RTC option
- run-time errors, error checks
- O compiler option, /RTC option
- debugger, runtime errors
- variables [debugger], loss of data
- runtime_checks pragma
- variables [debugger], catching dependencies on uninitialized local variables
- run-time errors, debugging
- debugger, native run-time checks
- optimized build option
- RTC compiler option, /O compiler option
- native run-time checks
- run-time checks
- debugging arrays
- stack pointers
- arrays [Visual Studio], debugging
ms.assetid: dc7b2f1e-5ff6-42e0-89b3-dc9dead83ee1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 70f047fa84513821812a13f7dee3136d2d431d9a
ms.sourcegitcommit: 993fca11dc373a10150751bc2a045a9701a9db2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98240245"
---
# <a name="how-to-use-native-run-time-checks"></a>方法: ネイティブ ランタイム チェックを使用する
Visual Studio C++ プロジェクトでは、ネイティブ [runtime_checks](/cpp/preprocessor/runtime-checks) を使用して、次のような一般的なランタイム エラーをキャッチできます。

- スタック ポインターの破損

- ローカル配列のオーバーラン

- スタックの破損

- 初期化されていないローカル変数への依存性

- 短い変数への代入によるデータの消失

  最適化された ( **/RTC** ) ビルドで **/O** を使用すると、コンパイラ エラーが発生します。 `runtime_checks` プラグマを最適化されたビルドに使用しても効果はありません。

  ランタイム チェックが有効になっている状態のプログラムをデバッグすると、既定の動作では、ランタイム エラーの発生時にプログラムが停止し、デバッガーが起動されます。 この既定の動作は、任意のランタイム チェックで変更できます。 詳細については、「[デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)」を参照してください。

  次の手順で、デバッグ ビルドでネイティブ ランタイム チェックを有効にする方法と、ネイティブ ランタイム チェックの動作を変更する方法を説明します。

  このセクションのその他のトピックでは、次の内容について説明します。

- [C ランタイム ライブラリによるネイティブ ランタイム チェックのカスタマイズ](../debugger/native-run-time-checks-customization.md)

### <a name="to-enable-native-run-time-checks-in-a-debug-build"></a>デバッグ ビルドでネイティブ ランタイム チェックを有効にするには

- **/RTC** オプションを使用して、C ランタイム ライブラリのデバッグ バージョン (/MDd など) とリンクします。

### <a name="to-modify-native-run-time-check-behavior"></a>ネイティブ ランタイム チェックの動作を変更するには

- `runtime_checks` プラグマを使用します。

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [ランタイム エラー チェック](/cpp/c-runtime-library/run-time-error-checking)