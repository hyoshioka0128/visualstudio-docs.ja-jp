---
title: セキュリティの問題 |Microsoft Docs
description: リモートデバッグや他のサービスが関係する状況など、Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e7b834dc41fb019e70aa40bca995770985d4c05
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960924"
---
# <a name="security-issues"></a>セキュリティの問題
Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可は、開発者がプログラムを実行するために必要とするものと同じです。 これには、ほとんどの状況でのリモートデバッグが含まれます。 インターネットインフォメーションサービスなど、他のサービスを含む状況によっては、より高いレベルの権限が必要になる場合があります。

 Visual Studio の実行中、プロセスデバッグマネージャー (PDM) はローカルコンピューター上のデバッグプロセスを追跡します。 リモートデバッグを処理し、PDM を利用できるようにするために、開発者が *msvsmon.exe* と呼ばれるプログラムをリモートで起動します。 (*msvsmon.exe* はサービスではないため、そのコンピューターでリモートデバッグを有効にするには、手動で開始する必要があります。)Visual Studio (または *msvsmon.exe*) が実行されていない場合、デバッグのためにプロセスは追跡されません。

 開発者は、特別なアクセス許可なしで開始したプログラムをデバッグできます。 開発者は、他のユーザーが同じセキュリティグループのメンバーである場合に、他のユーザーによって開始されたプロセスをデバッグすることもできます。 また、リモートデバッグを有効にするには、必要なファイルをリモートコンピューターにコピーして *msvsmon.exe* を開始するだけです。 詳細については、「[リモート デバッグ](../../debugger/remote-debugging.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
- [プロセスデバッグマネージャー](../../extensibility/debugger/process-debug-manager.md)
- [リモート デバッグ](../../debugger/remote-debugging.md)
