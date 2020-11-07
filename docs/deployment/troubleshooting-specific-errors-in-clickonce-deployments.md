---
title: エラーのトラブルシューティング (ClickOnce 配置)
description: この記事では、ClickOnce アプリケーションを配置するときに発生する可能性のある一般的なエラーについて説明し、各問題を解決するための手順を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.UncRequired
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.NoInstallUrl
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
ms.assetid: 22dfe8f1-8271-4708-9c25-6bbb13920ac8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: af462178cf18d57afa6b51aedaba0004615ebb6f
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349266"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>ClickOnce 配置の固有のエラーのトラブルシューティング
この記事では、アプリケーションを展開するときに発生する可能性がある一般的なエラー [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] と、それぞれの問題を解決するための手順を示します。

## <a name="general-errors"></a>一般エラー

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>アプリケーションファイルを検索しようとしたとき、Internet Explorer で何も実行されない、または XML が表示される、または [実行] または [名前を付けて保存] ダイアログボックスが表示される
 このエラーは、サーバーまたはクライアントにコンテンツの種類 (MIME の種類とも呼ばれます) が正しく登録されていないことが原因である可能性があります。

 まず、サーバーが、 *アプリケーション* の拡張子を "application/x-ms アプリケーション" に関連付けるように構成されていることを確認します。

 サーバーが正しく構成されている場合は、.NET Framework 2.0 がコンピューターにインストールされていることを確認します。 .NET Framework 2.0 がインストールされていても、この問題が解決しない場合は、.NET Framework 2.0 をアンインストールしてから再インストールし、クライアントにコンテンツの種類を再登録してみてください。

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>「アプリケーションを取得できません」というエラーメッセージが表示されます。 展開に見つからないファイル "または" アプリケーションのダウンロードが中断されました。ネットワークエラーを確認し、後でもう一度お試しください "
 このメッセージは、マニフェストによって参照されている1つ以上のファイルを [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ダウンロードできないことを示します。 このエラーをデバッグする最も簡単な方法は、ダウンロードできないという URL をダウンロードしようとすることです [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 次のような原因が考えられます。

- ログファイルに "(403) 許可されていません" または "(404) が見つかりません" と表示されている場合は、Web サーバーがこのファイルのダウンロードをブロックしないように構成されていることを確認します。 詳細については、「[ClickOnce 配置でのサーバーおよびクライアント構成の問題](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)」を参照してください。

- *.Config* ファイルがサーバーによってブロックされている場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] この記事の後半にある「.config ファイルを含むアプリケーションをインストールしようとすると、ダウンロードエラー」セクションを参照してください。

- このエラーが発生したかどうかを判断するに `deploymentProvider` は、配置マニフェスト内の url が、アクティブ化に使用される url とは異なる場所を指していることを確認します。

- すべてのファイルがサーバーに存在することを確認します。ログには、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 見つからなかったファイルが通知されます。

- ネットワーク接続に問題があるかどうかを確認します。ダウンロード中にクライアントコンピューターがオフラインになった場合は、このメッセージが表示されます。

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>.Config ファイルを含む ClickOnce アプリケーションをインストールしようとすると、ダウンロードエラーが発生する
 Windows ベースのアプリケーション Visual Basic には、既定で App.config ファイルが含まれています。 Windows Server 2003 を使用している Web サーバーからユーザーがをインストールしようとすると、問題が発生します。これは、セキュリティ上の理由から、オペレーティングシステムによって *.config* ファイルのインストールがブロックされるためです。 *.Config* ファイルをインストールできるようにするには、[ **発行オプション** ] ダイアログボックスの [ **.deploy] ファイル拡張子** をクリックします。

 また、アプリケーション、マニフェスト、および .deploy ファイルに対して、コンテンツの種類 (MIME の種類) を適切に設定する必要があります。 詳細については、Web サーバーのドキュメントを参照してください。

 詳細については、「 [ClickOnce 配置でのサーバーおよびクライアント構成の問題](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)」の「Windows Server 2003: ロックダウンされたコンテンツの種類」を参照してください。

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>エラーメッセージ: "アプリケーションの形式が正しくありません。"ログファイルに "XML 署名が無効です" が含まれています
 マニフェストファイルを更新し、再度署名したことを確認します。 を使用してアプリケーションを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 再発行するか、mage.exe を使用してアプリケーションに再度署名します。

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>サーバーでアプリケーションを更新しましたが、クライアントが更新プログラムをダウンロードしません。
 この問題は、次のいずれかのタスクを完了することで解決できる場合があります。

- `deploymentProvider`配置マニフェストの URL を確認します。 を指す同じ場所にあるビットを更新していることを確認し `deploymentProvider` ます。

- デプロイマニフェストで更新間隔を確認します。 この間隔が6時間ごとに1回などの定期的な間隔に設定されている場合、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、この間隔が経過するまで更新プログラムをスキャンしません。 アプリケーションが起動するたびに更新プログラムをスキャンするようにマニフェストを変更することができます。 更新間隔の変更は、更新プログラムがインストールされていることを確認するための開発時に便利なオプションですが、アプリケーションのアクティブ化の速度が低下します。

- [スタート] メニューでもう一度アプリケーションを起動してみてください。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] バックグラウンドで更新プログラムが検出された可能性がありますが、次回のライセンス認証時に bits をインストールするように求められます。

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>更新中に、"展開内の参照がアプリケーションマニフェストで定義されている id と一致しません" というログエントリを含むエラーが表示されます。
 このエラーは、配置マニフェストとアプリケーションマニフェストを手動で編集し、1つのマニフェスト内のアセンブリの id の説明が他のマニフェストと同期しなくなったことが原因で発生する可能性があります。 アセンブリの id は、名前、バージョン、カルチャ、および公開キートークンで構成されます。 マニフェスト内の id の説明を確認し、相違点を修正します。

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>ローカルディスクまたは CD-ROM からの初回のアクティブ化は成功しますが、[スタート] メニューからの後続のライセンス認証は成功しません。
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、展開プロバイダーの URL を使用して、アプリケーションの更新プログラムを受信します。 URL が指している場所が正しいことを確認します。

#### <a name="error-cannot-start-the-application"></a>エラー: "アプリケーションを起動できません"
 このエラーメッセージは、通常、このアプリケーションをストアにインストールするときに問題が発生したことを示して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] います。 アプリケーションでエラーが発生したか、ストアが破損しています。 ログファイルには、エラーが発生した場所が示される場合があります。

 次の操作を行う必要があります。

- デプロイマニフェストの id、アプリケーションマニフェストの id、およびメインアプリケーション EXE の id がすべて一意であることを確認します。

- ファイルパスが100文字を超えていないことを確認します。 アプリケーションに長すぎるファイルパスが含まれている場合は、格納できる最大パスの制限を超える可能性があります。 パスを短くして再インストールしてみてください。

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>アプリケーション構成ファイルの PrivatePath 設定は受け入れられません
 PrivatePath (Fusion プローブパス) を使用するには、アプリケーションが完全信頼のアクセス許可を要求する必要があります。 完全信頼を要求するようにアプリケーションマニフェストを変更してから、再試行してください。

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>アンインストール中に "アプリケーションをアンインストールできませんでした" というメッセージが表示される
 このメッセージは、通常、アプリケーションが既に削除されているか、ストアが破損していることを示しています。 [ **OK** ] をクリックすると、 **プログラムの追加と削除** のエントリが削除されます。

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>インストール中に、プラットフォームの依存関係がインストールされていないというメッセージが表示されます。
 アプリケーションが実行するために必要な必須コンポーネントが GAC (グローバルアセンブリキャッシュ) にありません。

## <a name="publishing-with-visual-studio"></a>Visual Studio を使用した発行

#### <a name="publishing-in-visual-studio-fails"></a>Visual Studio での発行が失敗する
 ターゲットとしているサーバーに発行する権限があることを確認します。 たとえば、管理者としてではなく、通常のユーザーとしてターミナルサーバーコンピューターにログインしている場合は、ローカル Web サーバーへの発行に必要な権限を持っていない可能性があります。

 URL を使用して発行する場合は、対象のコンピューターで FrontPage Server Extensions 有効になっていることを確認します。

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>エラーメッセージ: Web サイト ' ' を作成できません \<site> 。 FrontPage Server Extensions と通信するためのコンポーネントがインストールされていません。
 発行元のコンピューターに Microsoft Visual Studio Web オーサリングコンポーネントがインストールされていることを確認します。 Express ユーザーの場合、このコンポーネントは既定ではインストールされません。 詳細については、[http://go.microsoft.com/fwlink/?LinkId=102310](https://support.microsoft.com/help/945358) をご覧ください。

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>エラーメッセージ: ファイル ' 6.0.0.0, Version =, Culture = *, PublicKeyToken = 6595b64144ccf1df, ProcessorArchitecture = \* , Type = win32 ' が見つかりませんでした。
 このエラーメッセージは、visual スタイルが有効になっている WPF アプリケーションを公開しようとしたときに表示されます。 この問題を解決するには、「 [方法: Visual スタイルが有効になっている WPF アプリケーションを発行](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)する」を参照してください。

## <a name="using-mage"></a>Mage の使用

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>証明書ストアの証明書と、受信した空白のメッセージボックスを使用して署名しようとしました。
 [ **署名** ] ダイアログボックスで、次のことを行う必要があります。

- [ **保存された証明書で署名する** ] を選択します。

- 一覧から証明書を選択します。最初の証明書は、既定では選択されていません。

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>[署名しない] ボタンをクリックすると、例外が発生します。
 この問題は既知のバグです。 すべて [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のマニフェストが署名されている必要があります。 いずれかの署名オプションを選択し、[ **OK]** をクリックします。

## <a name="additional-errors"></a>その他のエラー
 次の表は、ユーザーがアプリケーションをインストールするときに、クライアントコンピューターのユーザーが受け取る可能性のある一般的なエラーメッセージを示して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] います。 各エラーメッセージは、エラーの最も可能性の高い原因の説明の横に一覧表示されます。

| エラー メッセージ | 説明 |
| - | - |
| アプリケーションを起動できません。 アプリケーションの発行元に問い合わせてください。<br /><br /> アプリケーションを起動できません。 詳細については、アプリケーションベンダーに問い合わせてください。 | これらは、アプリケーションを起動できず、その他の特定の理由が見つからない場合に発生する一般的なエラーメッセージです。 多くの場合、アプリケーションが破損しているか、ストアが破損していることを意味 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] します。 |
| 続行できません。 アプリケーションの形式が正しくありません。 詳細については、アプリケーションの発行元に問い合わせてください。<br /><br /> アプリケーションの検証に失敗しました。 続行できません。<br /><br /> アプリケーションファイルを取得できません。 配置でファイルが破損しています。 | 配置内のいずれかのマニフェストファイルの構文が正しくありません。または、対応するファイルと照合できないハッシュが含まれています。 このエラーは、アセンブリ内に埋め込まれているマニフェストが破損していることを示している場合もあります。 配置を再作成し、アプリケーションを再コンパイルするか、マニフェストでエラーを手動で見つけて修正します。 |
| アプリケーションを取得できません。 認証エラーです。<br /><br /> アプリケーションのインストールが成功しませんでした。 サーバー上のアプリケーションファイルが見つかりません。 詳細については、アプリケーションの発行元または管理者に問い合わせてください。 | 配置内の1つ以上のファイルをダウンロードできません。アクセスするためのアクセス許可がありません。 これは、Web サーバーから403の禁止エラーが返されたことが原因で発生する可能性があります。これは、配置内のいずれかのファイルが、Web サーバーで保護されたファイルとして扱われる拡張機能で終了した場合に発生することがあります。 また、アプリケーションのファイルが1つ以上含まれているディレクトリでは、にアクセスするためにユーザー名とパスワードが必要になる場合があります。 |
| アプリケーションをダウンロードできません。 アプリケーションに必要なファイルがありません。 詳細については、アプリケーションベンダーまたはシステム管理者にお問い合わせください。 | アプリケーションマニフェストに一覧表示されている1つ以上のファイルがサーバーに見つかりません。 すべての展開の依存ファイルがアップロードされていることを確認してから、操作をやり直してください。 |
| アプリケーションのダウンロードに失敗しました。 ネットワーク接続を確認するか、システム管理者またはネットワークサービスプロバイダーに問い合わせてください。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] サーバーへのネットワーク接続を確立できません。 サーバーの可用性とネットワークの状態を確認します。 |
| URLDownloadToCacheFile が HRESULT ' ' で失敗しました \<number> 。 ' ' のダウンロード中にエラーが発生しました \<file> 。 | 展開先のコンピューターで [Internet Explorer のセキュリティ強化モードを変更するときに警告する] オプションを設定している場合、およびインストールされている ClickOnce アプリケーションのセットアップ URL がセキュリティで保護されていないサイト (またはその逆) にリダイレクトされていると、Internet Explorer の警告によってインストールが失敗します。<br /><br /> このエラーを解決するには、次のいずれかのタスクを実行します。<br /><br /> -セキュリティオプションをオフにします。<br />-セットアップ URL が、セキュリティモードを変更するようにリダイレクトされていないことを確認します。<br />-リダイレクトを完全に削除し、実際のセットアップ URL をポイントします。 |
| ハードディスクへの書き込み中にエラーが発生しました。 ディスクに十分な空き領域がない可能性があります。 詳細については、アプリケーションベンダーまたはシステム管理者にお問い合わせください。 | これは、アプリケーションを格納するためのディスク領域が不足していることを示している可能性がありますが、アプリケーションファイルをドライブに保存しようとしているときに、より一般的な i/o エラーが発生することもあります。 |
| アプリケーションを起動できません。 ディスクに十分な空き領域がありません。 | ハードディスクがいっぱいです。 領域をオフにして、アプリケーションをもう一度実行してください。 |
| 一度に読み込もうとしている、展開されているアクティブ化の数が多すぎます。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 同時に開始できるさまざまなアプリケーションの数を制限します。 これは、ほとんどの場合、ローカルサービスに対するサービス拒否攻撃を防ぐために役立ち [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。同じアプリケーションを迅速に起動しようとすると、アプリケーションのインスタンスは1つだけになります。 |
| ネットワーク経由でショートカットをアクティブ化することはできません。 | アプリケーションへのショートカットは [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、ローカルハードディスク上でのみ開始できます。 リモートサーバー上のショートカットファイルを指す URL を開くことによって開始することはできません。 |
| アプリケーションが大きすぎて、部分信頼でオンラインで実行できません。 詳細については、アプリケーションベンダーまたはシステム管理者にお問い合わせください。 | 部分信頼で実行されるアプリケーションは、オンラインアプリケーションクォータの半分 (既定では 250 MB) より大きくすることはできません。 |

## <a name="see-also"></a>関連項目
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)