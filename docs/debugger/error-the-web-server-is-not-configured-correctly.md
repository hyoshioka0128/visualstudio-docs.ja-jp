---
title: エラー - Web サーバーが正しく構成されていません | Microsoft Docs
ms.date: 09/20/2017
ms.topic: error-reference
f1_keywords:
- vs.debug.remote.projnotconfigured
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 711297ef00c064c482ed3a86b896566b6e019534
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460326"
---
# <a name="error-the-web-server-is-not-configured-correctly"></a>エラー :Web サーバーは正しく構成されていません。

ここで説明されている手順を実行して問題を解決した後、デバッグを再試行する前に、IIS のリセットも必要な場合があります。 管理者のコマンド プロンプトを開き、「`iisreset`」と入力することで、これを行うことができます。

この問題を解決するには、次の手順に従ってください。

1. サーバーでホストされている Web アプリがリリース ビルドとして構成されている場合は、デバッグ ビルドとして再発行し、web.config ファイルにコンパイル要素の `debug=true` が含まれていることを確認します。 IIS をリセットして、再試行します。

    たとえば、リリース ビルドに対して発行プロファイルを使用している場合は、デバッグに変更してから再発行します。 そうしないと、発行時に debug 属性に `false` が設定されます。

2. (IIS) 物理パスが正しいことを確認します。 IIS では、 **[基本設定] > [物理パス]** (IIS の古いバージョンでは **[詳細設定]** ) でこの設定を見つけることができます。

    Web アプリケーションが別のコンピューターにコピーされた、手動で名前が変更された、または別の場所に移動された場合は、物理パスが違っている可能性があります。 IIS をリセットして、再試行します。

3. Visual Studio でローカルにデバッグしている場合は、プロパティに正しいサーバーが選択されていることを確認します (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** を開きます。 Web フォーム プロジェクトの場合は、 **[プロパティ ページ] > [起動オプション] > [サーバー]** を開きます)。

    IIS などの外部 (カスタム) サーバーを使用している場合は、正しい URL が必要です。 それ以外の場合は、[IIS Express] を選択して再試行します。

4. (IIS) ASP.NET の正しいバージョンがサーバーにインストールされていることを確認します。

    ASP.NET の IIS 上のバージョンと Visual Studio プロジェクト内のバージョンの不一致によって、この問題が発生することがあります。 web.config 内にフレームワークのバージョンの設定が必要な可能性があります。IIS に ASP.NET をインストールするには、[Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) を使用します。 「[ASP.NET 3.5 と ASP.NET 4.5 を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」も参照してください。ASP.NET Core の場合は、「[IIS を使用して Windows でホストする](https://docs.asp.net/en/latest/publishing/iis.html)」を参照してください。

4. IIS の `maxConnection` 制限が低いときに、接続数が多い場合は、[接続制限の増加](/iis/configuration/system.applicationhost/sites/sitedefaults/limits)が必要である可能性があります。

## <a name="see-also"></a>関連項目
- [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)
- [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)