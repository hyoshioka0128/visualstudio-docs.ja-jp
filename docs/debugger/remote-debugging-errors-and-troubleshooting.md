---
title: リモート デバッグのエラーとトラブルシューティング | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, errors
- debugging errors
- remote debugging, troubleshooting
- troubleshooting remote debugging
- errors [debugger], remote debugging
- remote debugging, errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b413ce193e6761d515de5bc5ef30fae8e18a3a3
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301069"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>リモート デバッグ エラーとトラブルシューティング

デバッグをリモートで試行した場合に、次のエラーが発生することがあります。

- [エラー: サーバーに自動的にステップ インできません](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [エラー: Microsoft Visual Studio リモート デバッグ モニター (MSVSMON.EXE) は、リモート コンピューター上では実行されていません。](error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running.md)

- [Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [エラー: リモート コンピューターが [リモート接続] ダイアログに表示されません](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>管理者としてリモート デバッガーを実行する

リモート デバッガーを管理者として実行しないと、問題が発生する可能性があります。 たとえば、次のエラーが表示される場合があります: "Visual Studio リモート デバッガー (MSVSMON.EXE) には、このプロセスをデバッグする十分な特権がありません。" リモート デバッガーを (サービスではなく) アプリケーションとして実行している場合は、[別のユーザー アカウント](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md) エラーが表示されることがあります。

### <a name="when-running-the-remote-debugger-as-a-service"></a>サービスとしてリモート デバッガーを実行する場合

リモート デバッガーをサービスとして実行するときは、いくつかの理由から管理者として実行することをお勧めします。

- リモート デバッガー サービスでは管理者からの接続のみが許可されるので、管理者として実行することによって発生する新しいセキュリティ リスクは**ありません**。

- プロセスをデバッグするために、リモート デバッガー自体より多くの権限を Visual Studio ユーザーが持つことにより発生するエラーを防ぐことができます。

- リモート デバッガーのセットアップと構成が簡単になります。

リモート デバッガーを管理者として実行しなくてもデバッグはできますが、これを正しく動作させるにはいくつかの要件があり、多くの場合、より高度なサービス構成手順が必要になります。

- リモート コンピューターで使用しているアカウントには、**サービスとしてログオン**特権が必要です。 [接続できない場合](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)のエラー記事の "サービスとしてログオンの追加" に関する手順を参照してください。

- アカウントには、ターゲット プロセスをデバッグするための権限が必要です。 これらの権限を取得するには、デバッグ対象のプロセスと同じアカウントでリモート デバッガーを実行する必要があります。 (代わりの簡単な方法は、管理者としてサービスを実行することです)。 

- アカウントは、ネットワーク経由で Visual Studio コンピューターに接続できる (つまり、認証できる) 必要があります。 ドメインでは、リモート デバッガーが組み込みのローカル システム アカウントかネットワーク サービス アカウント、またはドメイン アカウントで実行されている場合、接続が簡単になります。 組み込みアカウントには、セキュリティ リスクになる可能性がある、管理者特権でのセキュリティ特権があります。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>リモート デバッガーをアプリケーションとして実行する場合 (通常モード)

(通常のアプリケーションなど) 独自の管理者特権ではないプロセスにアタッチしようとする場合は、リモート デバッガーを管理者として実行しているかどうかは関係ありません。

次のようないくつかのシナリオでは、管理者としてリモート デバッガーを実行する必要があります。

- 別のユーザーとして実行されているプロセスにアタッチする場合 (IIS のデバッグ時など)。

- 別のプロセスを起動しようとしていて、起動するプロセスが管理者である場合。

プロセスを起動し、起動するプロセスが管理者である必要が**ない**場合は、管理者として実行する必要は**ありません**。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)