---
title: 例外後の実行の継続 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e94867d845988b787247c32d32afd35af946972
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350681"
---
# <a name="continuing-execution-after-an-exception"></a>例外後の実行の継続
例外が発生したためにデバッガーの実行が中断されると、既定で **[例外ヘルパー]** が表示されます。 **[オプション]** ダイアログ ボックスで **[例外ヘルパー]** を無効にしている場合は、 **[例外アシスタント]** (C# または Visual Basic) または **[例外]** ダイアログ ボックス (C++) が表示されます。

 **[例外ヘルパー]** が表示されたら、例外の原因となった問題の修正を試みることができます。

## <a name="managed-and-native-code"></a>マネージド コードとネイティブ コード
 マネージド コードとネイティブ コードでは、未処理の例外の後に同じスレッドで実行を継続できます。 **[例外ヘルパー]** では、例外がスローされた時点まで呼び出し履歴を戻すことができます。

## <a name="mixed-code"></a>混合コード
 ネイティブ コードとマネージド コードが混在するコードをデバッグしているときに、ハンドルされていない例外が発生した場合、オペレーティング システムの制約により、呼び出し履歴のアンワインドが抑制されます。 ショートカット メニューを使用して呼び出し履歴をさかのぼろうとすると、混合コードのデバッグ中は、ハンドルされていない例外からアンワインドすることはできないという内容のエラー メッセージが表示されます。

## <a name="see-also"></a>関連項目

- [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)