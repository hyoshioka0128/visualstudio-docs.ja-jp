---
title: ネイティブ ランタイム チェックのカスタマイズ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.crt
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- runtime_checks pragma
- debugger, native run-time checks
- /RTC compiler option [C++], native run-time checks
- customizing CRT error checking
- native run-time checks, customizing
ms.assetid: 76a365fe-6439-49db-8603-34058b78e5a8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: db7cc513c4c96a8b60cc6471280bb837a7b9a248
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72730898"
---
# <a name="native-run-time-checks-customization"></a>ネイティブ ランタイム チェックのカスタマイズ
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
 `_RTC_NumErrors` は、ランタイム エラー チェックで検出されたエラーの種類の数を返します。 各エラーの簡単な説明を取得するには、0 ～ `_RTC_NumErrors` の戻り値をループし、各ループで `_RTC_GetErrDesc` に反復値を渡すことができます。 詳細については、「[_RTC_NumErrors](/cpp/c-runtime-library/reference/rtc-numerrors)」と「[_RTC_GetErrDesc](/cpp/c-runtime-library/reference/rtc-geterrdesc)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: ネイティブ ランタイム チェックを使用する](../debugger/how-to-use-native-run-time-checks.md)
- [runtime_checks](/cpp/preprocessor/runtime-checks)
- [_CrtDbgReport、_CrtDbgReportW](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw)