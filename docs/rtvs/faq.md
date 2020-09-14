---
title: R Tools for Visual Studio の FAQ
description: Visual Studio での R に関してよく寄せられる質問です。
ms.date: 12/04/2017
ms.topic: reference
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 8c89f1d59405fb7475e827cac9624c6623d7041e
ms.sourcegitcommit: 1d74273a50ede5a90d9d64372d93aad357daef42
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89365666"
---
# <a name="frequently-asked-questions"></a>よく寄せられる質問

## <a name="visual-studio-support"></a>Visual Studio のサポート

**Q.RTVS は OS X または Linux で動作しますか?**

A. RTVS は現在 Visual Studio で動作するように設計されているため、Windows 限定の実装になります。 Microsoft では、Visual Studio Code および Visual Studio for Mac でのサポートを調査中です。 [RTVS の Issue #1295](https://github.com/Microsoft/RTVS/issues/1295) を参照してください。

**Q.RTVS は Visual Studio Express Edition で動作しますか?**

A. いいえ。

**Q.RTVS で Visual Studio の拡張機能を使用できますか?**

A. もちろんです。 以下に R を使用するユーザーに人気の拡張機能を示しますが、これらはごく一部です。

- [VsVim で Vim のキー バインド](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)
- [GitHub](https://marketplace.visualstudio.com/items?itemName=GitHub.GitHubExtensionforVisualStudio)
- [Markdown editor によるライブ プレビュー](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.MarkdownEditor)

詳細については、[Visual Studio Marketplace](https://marketplace.visualstudio.com/) をご覧ください。

**Q.RTVS を Visual Studio 内にインストールするのですから、R を C# や C++ などの Microsoft 言語と合わせて簡単に使用できますか?**

A. いいえ。 RTVS は R コードの開発ツールであり、R の標準的なネイティブ インタープリターを使用します。 R と他の言語との相互運用はサポートされていません。

**Q.RTVS は英語以外のロケールで機能しますか?**

A. RTVS の 1.0 リリースは英語版のみです。 1.1 リリースでは、Visual Studio と同じ言語セットにローカライズされる予定です。 それまでは、[Visual Studio 2015 用の英語の言語パック](https://www.microsoft.com/download/details.aspx?id=48157)を使用するか、Visual Studio 2017 でインストーラーを実行し、**[言語パック]** タブで [英語] を選択してください。

![Visual Studio 2017 の各国対応設定](media/FAQ-international-settings.png)

**Q.現在の Visual Studio の設定を本当に気に入っていますが、新しいデータ サイエンスの設定も試してみたいです。どうしたらいいのでしょうか?**

A. **[ツール]** の **[設定のインポートとエクスポート]** を使用して現在の Visual Studio 設定を保存し、次にデータ サイエンスの設定に切り替えます。 保存した設定を復元するには、**[設定のインポートとエクスポート]** コマンドを再度使用します。

**Q.ネットワーク共有上で Visual Studio プロジェクトを保存できますか?**

A. いいえ。Visual Studio では、ネットワーク共有からのプロジェクトの読み込みをサポートしていません。

## <a name="r-interpretersintegration"></a>R インタープリター/統合

**Q.RTVS で使用可能な R インタープリターにはどのようなものがありますか?**

A. [CRAN R](https://cran.r-project.org/)、[Microsoft R Client、Microsoft Machine Learning Server](/machine-learning-server/) が使用できます。

**Q.これらのインタープリターはどこでダウンロードできますか?**

A. [インストール](installing-r-tools-for-visual-studio.md)に関する記事をご覧ください。

**Microsoft R Server とは何ですか?**

A. R Server の以前の名前は、[Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server) です。

**Q.RTVS で R の 32 ビット エディションを使用できますか?**

A. いいえ。RTVS では、Windows の 64 ビット エディションで動作する R の 64 ビット エディションのみがサポートされます。

**Q.RTVS ではソース管理システムを利用できますか?**

A. はい。Visual Studio に統合されている任意のソース管理システムを使用できます。

**Q.RTVS プロジェクトで推奨される *.gitignore* の設定はどのようなものですか?**

A. GitHub には、推奨される *.gitignore* ファイルのリポジトリがあります。 [R .gitignore](https://github.com/github/gitignore/blob/master/R.gitignore) をご覧ください。

## <a name="remote-services"></a>リモート サービス

Q. **Visual Studio のリモート サービスとは?**

A. Remote R Services for Visual Studio を使用すると、Windows または Linux のコンピューターをセットアップし、RTVS から接続することができます。 「[リモート ワークスペースの設定](setting-up-remote-r-workspaces.md)」を参照してください。

Q. **RTVS は Microsoft Machine Learning Server に接続できますか?**

A. いいえ。Microsoft ML Server は異なるテクノロジを採用しており、RTVS で必要とされる接続メカニズムを備えていません。

Q. **RTVS は Azure 上でデータ サイエンス VM イメージを使用して作成された VM に接続できますか?**

A. はい。[データ サイエンス VM - Windows 2016](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) イメージは、Remote R Services for Visual Studio にプレインストールされています。

Q: **RTVS は R がインストールされているリモート コンピューターに接続できますか?**

リモート コンピューター上で R コードを実行するには、要求をリッスンし、コードを受信し、クライアント コンピューターに結果を返送する何らかのサービスが必要です。 このサービスは、Remote R Services for Visual Studio によって提供されます。 「[リモート ワークスペースの設定](setting-up-remote-r-workspaces.md)」を参照してください。

Q. **リモート セッションとは何ですか?**

A. Machine Learning Server のドキュメントに掲載されている[リモート サーバーでの実行](/machine-learning-server/r/how-to-execute-code-remotely)に関する記事を参照してください。

## <a name="rtvs-development-and-features"></a>RTVS の開発と機能

**Q.RStudio に用意されている機能 X がありません。**

A. RStudio は完成度の高いすばらしい R 用の IDE であり、長年にわたり開発されています。 作業を適切に行う上で重要な機能すべてを RTVS に搭載するように開発を進めています。 [GitHub](https://github.com/Microsoft/RTVS/issues/) でイシューを登録すると、将来の作業の優先順位を高くするのに役立ちます。

**Q.RTVS に貢献できますか?**

A. もちろんあります。 ソース コードは [Github](https://github.com/microsoft/RTVS) で公開されています。 問題の追跡ツールを使用して、すでに存在するファイルに対するバグ情報とコメントをお寄せください。

このドキュメントに対する投稿も歓迎しています。&mdash;ページの右上の **[編集]** を選択してください。 また、ページの最下部から、ドキュメントに対するコメントもお寄せください。
