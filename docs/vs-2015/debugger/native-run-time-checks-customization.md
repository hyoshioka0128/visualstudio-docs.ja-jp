---
title: ネイティブ ランタイム チェックのカスタマイズ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
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
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 434f2425b1eeefd82b954e47a8ced55491a7ec11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697817"
---
# <a name="native-run-time-checks-customization"></a>ネイティブ ランタイム チェックのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**/RTC** (ランタイム チェック) を使用してコンパイルするか、`runtime_checks` プラグマを使用すると、C ランタイム ライブラリによってネイティブ ランタイム チェックが提供されます。 ランタイム チェックのカスタマイズが必要になる場合があります。次に例を示します。  
  
- ランタイム チェック メッセージを既定とは異なるファイルや出力先に転送する。  
  
- サードパーティ デバッガーでのランタイム チェック メッセージの出力先を指定する。  
  
- C ランタイム ライブラリのリリース バージョンでコンパイルされたプログラムからのランタイム チェック メッセージを報告する。 ライブラリのリリース バージョンでは、ランタイム エラーの報告に `_CrtDbgReportW` は使用されません。 代わりに、ランタイム エラーごとに **[Assert]** ダイアログ ボックスが表示されます。  
  
  ランタイム エラー チェックをカスタマイズするには、次の方法があります。  
  
- ランタイム エラー レポート関数の記述 詳細については、[ランタイム エラー レポート関数を記述する](../debugger/how-to-write-a-run-time-error-reporting-function.md)」を参照してください。  
  
- エラー メッセージ出力先のカスタマイズ  
  
- ランタイム チェック エラーに関する情報のクエリ  
  
## <a name="customize-the-error-message-destination"></a>エラー メッセージ出力先のカスタマイズ  
 エラー レポートに `_CrtDbgReportW` を使用する場合は、`_CrtSetReportMode` を使用してエラー メッセージの出力先を指定できます。  
  
 カスタムのレポート関数を使用している場合、エラーとレポートの種類を関連付けるには、`_RTC_SetErrorType` を使用します。  
  
## <a name="query-for-information-about-run-time-checks"></a>ランタイム チェック情報のクエリ  
 `_RTC_NumErrors` は、ランタイム エラー チェックで検出されたエラーの種類の数を返します。 各エラーの簡単な説明を取得するには、0 ～ `_RTC_NumErrors` の戻り値をループし、各ループで `_RTC_GetErrDesc` に反復値を渡すことができます。 詳細については、「[_RTC_NumErrors](https://msdn.microsoft.com/library/7e82adae-38e2-4f8b-bc0b-37bda8109fd1)」と「[_RTC_GetErrDesc](https://msdn.microsoft.com/library/7994ec2b-5488-4fd4-806d-a166c9a9f927)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [方法: ネイティブランタイムチェックを使用する](../debugger/how-to-use-native-run-time-checks.md)   
 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b)   
 [_CrtDbgReport、_CrtDbgReportW](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc)
