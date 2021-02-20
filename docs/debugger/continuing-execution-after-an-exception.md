---
title: 例外後の実行の継続 | Microsoft Docs
description: 未処理の例外が原因でデバッガーの実行が中断されるとどうなるかについて説明します。 同じスレッドで実行を継続できる場合があります。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9af71aba1b26c3d8160af229d8c050038800106a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99865814"
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