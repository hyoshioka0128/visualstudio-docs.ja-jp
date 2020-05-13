---
title: セキュリティの問題 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40898f5633eac374206ed40bfcac96d9c1c5b753
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713049"
---
# <a name="security-issues"></a>セキュリティの問題
Visual Studio を使用してプログラムをデバッグするには、開発者がプログラムを実行するために必要なアクセス許可と同じアクセス許可のみが必要です。 これには、ほとんどの状況でリモート デバッグが含まれます。 インターネット インフォメーション サービスなどの他のサービスを含む状況によっては、より高いレベルのアクセス許可が必要な場合があります。

 Visual Studio の実行中、プロセス デバッグ マネージャー (PDM) は、ローカル コンピューター上のデバッグ プロセスを追跡します。 リモートからは、開発者がリモート デバッグを処理し、PDM を使用できるように *、msvsmon.exe*というプログラムが起動します。 (*msvsmon.exe*はサービスではないので、そのコンピュータでリモート デバッグを有効にするには手動で起動する必要があります ) 。Visual Studio (または*msvsmon.exe)* が実行されていない場合、デバッグ用に追跡されるプロセスはありません。

 開発者は、特別なアクセス許可を持たないプログラムをデバッグできます。 開発者は、他のユーザーが同じセキュリティ グループのメンバーである場合、他のユーザーによって開始されたプロセスをデバッグすることもできます。 また、リモート デバッグを有効にするには、必要なファイルをリモート コンピュータにコピーし、 *msvsmon.exe*を起動するだけで済みます。 詳細については、「[リモート デバッグ](../../debugger/remote-debugging.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
- [プロセス デバッグ マネージャー](../../extensibility/debugger/process-debug-manager.md)
- [リモート デバッグ](../../debugger/remote-debugging.md)
