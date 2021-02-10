---
title: デバッグ履歴 | Microsoft Docs
description: アプリの実行を前後に移動しながらその状態を調べることで、アプリのトラブルシューティングを行います。 Intellitrace によって、この機能の情報を収集します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7cc5ddf2-2f7c-4f83-b7ca-58e92e9bfdd2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c4a6bf07cc7905fc48bcc82c8b38fa5b6f6e7cfa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99904413"
---
# <a name="historical-debugging-c-visual-basic-c"></a>デバッグ履歴 (C#、Visual Basic、C++)

デバッグ履歴は、IntelliTrace で収集された情報に依存するデバッグのモードです。 アプリケーションの実行内を前後に移動して、実行の状態を調べることができます。

 IntelliTrace は Visual Studio Enterprise Edition で使用できます (Professional Edition または Community Edition の場合は使用できません)。

## <a name="why-use-historical-debugging"></a>デバッグ履歴を使用する理由

 ブレークポイントを設定してバグを探すのは、どちらかというと行き当たりばったりな方法です。 バグがありそうな場所のコードの近くにブレークポイントを設定し、デバッガーでアプリケーションを実行して、ブレークポイントがヒットし、実行が中断した場所でバグの原因が明らかになることを期待します。 原因がわからない場合は、コードの別の場所にブレークポイントを設定し、デバッガーを再実行して、問題が見つかるまで繰り返しテスト手順を行う必要があります。

 ![ブレークポイントの設定](../debugger/media/breakpointprocesa.png "BreakpointProcesa")

 IntelliTrace とデバッグ履歴を使用すると、アプリケーション内を移動して状態を調べることができ (呼び出し履歴およびローカル変数)、ブレークポイントを設定し、デバッグを再実行し、テスト手順を繰り返す必要はありません。 これにより多くの時間を節約できます。実行に時間がかかるテスト シナリオの深い場所にバグがある場合は特に有効です。

## <a name="how-do-i-start-using-historical-debugging"></a>デバッグ履歴の使用を始める方法

IntelliTrace は既定で有効になります。 必要なのは、自分にとって興味のあるイベントと関数呼び出しを決定し、アプリケーション状態の完全なスナップショットを表示するかどうかを決定するだけです。 調べる対象の定義について詳しくは、「[IntelliTrace の機能](../debugger/intellitrace-features.md)」をご覧ください。 機能のサポートは言語とアプリの種類によって異なります。

- デバッグ履歴でスナップショットを表示するには、[IntelliTrace を使用した以前のアプリの状態の調査](../debugger/view-historical-application-state.md)に関するページを参照してください。
- 変数を検査し、コード間を移動する方法については、[デバッグ履歴を使用したアプリの検査](../debugger/historical-debugging-inspect-app.md)に関するページを参照してください。
- IntelliTrace イベントを使用したデバッグの詳細については、[チュートリアル:IntelliTrace の使用](../debugger/walkthrough-using-intellitrace.md)に関するページを参照してください。