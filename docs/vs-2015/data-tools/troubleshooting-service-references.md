---
title: サービス参照のトラブルシューティング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: reference
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 60f06aa64cf6a6b96f0c4d610fba1d20b794c55f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667207"
---
# <a name="troubleshooting-service-references"></a>サービス参照のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
このトピックでは、でまたはを参照するときに発生する可能性のある一般的な問題を示し [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

## <a name="error-returning-data-from-a-service"></a>サービスからデータを取得中にエラーが発生した
 `DataSet`サービスからまたはを返すと、 `DataTable` "受信メッセージの最大サイズクォータを超えました" という例外が発生することがあります。 既定では、 `MaxReceivedMessageSize` 一部のバインドのプロパティは比較的小さい値に設定され、サービス拒否攻撃への影響を制限します。 この値は、例外を回避するために増やすことができます。

 このエラーを修復するには:

1. **ソリューションエクスプローラー**で、app.config ファイルをダブルクリックして開きます。

2. プロパティを見つけ `MaxReceivedMessageSize` て、それより大きい値に変更します。

## <a name="cannot-find-a-service-in-my-solution"></a>ソリューションでサービスが見つかりません
 [**サービス参照の追加**] ダイアログボックスの [**検出**] ボタンをクリックすると、ソリューション内の1つ以上の WCF サービスライブラリプロジェクトがサービスの一覧に表示されません。 これは、サービスライブラリがソリューションに追加されていても、まだコンパイルされていない場合に発生する可能性があります。

 このエラーを修復するには:

- **ソリューションエクスプローラー**で、[WCF サービスライブラリ] プロジェクトを右クリックし、[**ビルド**] をクリックします。

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>リモートデスクトップ経由でのサービスへのアクセスエラー
 ユーザーがリモートデスクトップ接続を介して Web ホスト WCF サービスにアクセスするときに、ユーザーに管理者権限がない場合は、NTLM 認証が使用されます。 ユーザーが管理アクセス許可を持っていない場合、"HTTP 要求は、クライアント認証スキーム ' Anonymous ' で許可されていません。" というエラーメッセージが表示されることがあります。 サーバーから受信した認証ヘッダーは ' NTLM ' でした。 "

 このエラーを修復するには:

1. Web サイトプロジェクトで、[ **プロパティ** ] ページを開きます。

2. [ **開始オプション** ] タブで、[ **NTLM 認証** ] チェックボックスをオフにします。

    > [!NOTE]
    > WCF サービスを排他的に含む Web サイトの NTLM 認証のみを無効にする必要があります。 WCF サービスのセキュリティは、web.config ファイルの構成によって管理されます。 これにより、NTLM 認証は不要になります。

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>生成されたクラス設定のアクセスレベルは無効です
 [**サービス参照の構成**] ダイアログボックスの [**生成されたクラスのアクセスレベル**] オプションを [**内部**] または [ **Friend** ] に設定すると、必ずしも機能しないことがあります。 このオプションはダイアログボックスで設定されているように見えますが、結果として得られるサポートクラスはのアクセスレベルで生成され `Public` ます。

 これは、を使用してシリアル化されるなど、特定の型の既知の制限です <xref:System.Xml.Serialization.XmlSerializer> 。

## <a name="error-debugging-service-code"></a>サービスコードのデバッグエラー
 クライアントコードから WCF サービスのコードにステップインすると、シンボルの不足に関連するエラーが表示されることがあります。 これは、ソリューションの一部であったサービスがソリューションから移動または削除されたときに発生する可能性があります。

 現在のソリューションの一部である WCF サービスに最初に参照を追加すると、サービスプロジェクトとサービスクライアントプロジェクトの間に明示的なビルド依存関係が追加されます。 これにより、クライアントが常に最新のサービスバイナリにアクセスすることが保証されます。これは、クライアントコードからサービスコードへのステップ実行などのデバッグシナリオに特に重要です。

 サービスプロジェクトがソリューションから削除された場合、この明示的なビルド依存関係は無効になります。 Visual Studio では、必要に応じてサービスプロジェクトが再構築されることを保証できなくなりました。

 このエラーを修正するには、サービスプロジェクトを手動でリビルドする必要があります。

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. [ **オプション** ] ダイアログボックスで、[ **プロジェクトおよびソリューション**] を展開し、[ **全般**] を選択します。

3. [ **ビルド構成の詳細を表示** する] チェックボックスがオンになっていることを確認し、[ **OK**] をクリックします。

4. WCF サービスプロジェクトを読み込みます。 詳細については、「 [NIB 方法: 複数のプロジェクトから成るソリューションを作成](https://msdn.microsoft.com/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)する」を参照してください。

5. [ **Configuration Manager** ] ダイアログボックスで、 **アクティブなソリューション構成** を [ **デバッグ**] に設定します。 詳細については、「 [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)」を参照してください。

6. **ソリューションエクスプローラー**で、WCF サービスプロジェクトを選択します。

7. [ **ビルド** ] メニューの [ **リビルド** ] をクリックして、WCF サービスプロジェクトをリビルドします。

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>ブラウザーに WCF Data Services が表示されない
 でデータの XML 表現を表示しようとすると [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 、Internet Explorer によってデータが RSS フィードとして誤って解釈されることがあります。 RSS フィードを表示するオプションが無効になっていることを確認してください。

 このエラーを解決するには、RSS フィードを無効にします。

1. Internet Explorer で、**[ツール]** メニューの **[インターネット オプション]** をクリックします。

2. [ **コンテンツ** ] タブの [ **フィード** ] セクションで、[ **設定**] をクリックします。

3. [ **フィードの設定** ] ダイアログボックスで、[ **フィードの読み取りビューを有効にする** ] チェックボックスをオフにし、[ **OK**] をクリックします。

4. [ **OK** ] をクリックして、[ **インターネットオプション** ] ダイアログボックスを閉じます。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio でのサービスと WCF Data Services の Windows Communication Foundation](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)