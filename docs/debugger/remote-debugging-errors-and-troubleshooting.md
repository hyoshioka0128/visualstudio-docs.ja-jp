---
title: リモート デバッグエラーとトラブルシューティング |マイクロソフトドキュメント
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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301069"
---
# <a name="remote-debugging-errors-and-troubleshooting"></a>リモート デバッグ エラーとトラブルシューティング

リモートでデバッグしようとすると、次のエラーが発生する可能性があります。

- [エラー : サーバーに自動的にステップ インできません。](../debugger/error-unable-to-automatically-step-into-the-server.md)

- [エラー : Microsoft Visual Studio リモート デバッグ モニター (MSVSMON.EXE) は、リモート コンピューター上では実行されていません。](error-remote-debugging-monitor-msvsmon-exe-does-not-appear-to-be-running.md)

- [リモート デバッグ モニターに接続できません。](../debugger/unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor.md)

- [エラー: リモート コンピューターが [リモート接続] ダイアログに表示されません](../debugger/error-remote-machine-does-not-appear-in-a-remote-connections-dialog.md)

## <a name="run-the-remote-debugger-as-an-administrator"></a>リモート デバッガーを管理者として実行する

リモート デバッガーを管理者として実行しないと、問題が発生する可能性があります。 たとえば、次のエラーが表示される可能性があります: "Visual Studio リモート デバッガー (MSVSMON.EXE) には、このプロセスをデバッグするための十分な特権がありません。 リモート デバッガーをアプリケーションとして実行している場合 (サービスではなく)、[ユーザー アカウントのエラーが表示](error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user.md)されることがあります。

### <a name="when-running-the-remote-debugger-as-a-service"></a>リモート デバッガーをサービスとして実行する場合

リモート デバッガーを s サービスとして実行する場合は、次のような理由から管理者として実行することをお勧めします。

- リモート デバッガー サービスでは、管理者からの接続のみが許可されるため、管理者として実行することによって新たに発生するセキュリティ リスク**はありません**。

- Visual Studio ユーザーがリモート デバッガー自体よりもプロセスをデバッグする権限を持っている場合に発生するエラーを防ぐことができます。

- リモート デバッガーのセットアップと構成を簡略化します。

リモート デバッガーを管理者として実行せずにデバッグすることは可能ですが、この作業を正しく行うにはいくつかの要件があり、多くの場合、より高度なサービス構成手順が必要になります。

- リモート コンピュータで使用しているアカウントには、**サービスとしてのログオン**特権が必要です。 「[接続できない](error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md)エラー」の「サービスとしてログオンを追加するには」の手順を参照してください。

- アカウントには、ターゲット プロセスをデバッグする権限が必要です。 これらの権限を取得するには、デバッグするプロセスと同じアカウントでリモート デバッガーを実行する必要があります。 (簡単な方法は、管理者としてサービスを実行することです)。 

- アカウントは、ネットワーク経由で Visual Studio コンピューターに接続できる (つまり、認証を使用して) できる必要があります。 ドメインでは、リモート デバッガーが組み込みのローカル システム アカウントまたはネットワーク サービス アカウント、またはドメイン アカウントで実行されている場合は、簡単に接続できます。 ビルトイン アカウントには、セキュリティリスクを引き起こす可能性のあるセキュリティ特権が昇格されています。

### <a name="when-running-the-remote-debugger-as-an-application-normal-mode"></a>リモート デバッガをアプリケーションとして実行する場合 (通常モード)

独自の非昇格プロセス (通常のアプリケーションなど) にアタッチしようとしている場合は、管理者としてリモート デバッガーを実行しているかどうかは問題ではありません。

リモート デバッガーを管理者として実行する場合は、次のようなシナリオがあります。

- 別のユーザーとして実行されているプロセス (IIS のデバッグ時など) にアタッチする場合、

- 別のプロセスを起動しようとしていますが、起動するプロセスは管理者です。

プロセスを起動する場合は管理者として実行**したくない**ため、起動するプロセスを管理者**に**することはできません。

## <a name="see-also"></a>関連項目
- [リモート デバッグ](../debugger/remote-debugging.md)