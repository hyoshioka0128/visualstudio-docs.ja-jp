---
title: '方法: ネイティブ ランタイム チェックを使用する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- c.runtime.errorchecks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
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
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b50dda3e31e27fa5d177c3b0ba2790babd2a660f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65685851"
---
# <a name="how-to-use-native-run-time-checks"></a>方法: ネイティブ ランタイム チェックを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ では、ネイティブ [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b) を使用して、次のような一般的なランタイム エラーをキャッチできます。  
  
- スタック ポインターの破損  
  
- ローカル配列のオーバーラン  
  
- スタックの破損  
  
- 初期化されていないローカル変数への依存性  
  
- 短い変数への代入によるデータの消失  
  
  最適化された ( **/RTC** ) ビルドで **/O**を使用すると、コンパイラ エラーが発生します。 `runtime_checks` プラグマを最適化されたビルドに使用しても効果はありません。  
  
  ランタイム チェックが有効になっている状態のプログラムをデバッグすると、既定の動作では、ランタイム エラーの発生時にプログラムが停止し、デバッガーが起動されます。 この既定の動作は、任意のランタイム チェックで変更できます。 詳細については、「[デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)」を参照してください。  
  
  次の手順で、デバッグ ビルドでネイティブ ランタイム チェックを有効にする方法と、ネイティブ ランタイム チェックの動作を変更する方法を説明します。  
  
  このセクションのその他のトピックでは、次の内容について説明します。  
  
- [C ランタイム ライブラリによるネイティブ ランタイム チェックのカスタマイズ](../debugger/native-run-time-checks-customization.md)  
  
- [C ランタイム ライブラリなしのランタイム チェックの使用方法](../debugger/using-run-time-checks-without-the-c-run-time-library.md)  
  
### <a name="to-enable-native-run-time-checks-in-a-debug-build"></a>デバッグ ビルドでネイティブ ランタイム チェックを有効にするには  
  
- **/RTC** オプションを使用して、C ランタイム ライブラリのデバッグ バージョン (/MDd など) とリンクします。  
  
### <a name="to-modify-native-run-time-check-behavior"></a>ネイティブ ランタイム チェックの動作を変更するには  
  
- `runtime_checks` プラグマを使用します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)   
 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b)   
 [ランタイム エラー チェック](https://msdn.microsoft.com/library/c965dd01-57ad-4a3c-b1d6-5aa04f920501)
