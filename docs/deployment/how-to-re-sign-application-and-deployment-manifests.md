---
title: '方法 : アプリケーション マニフェストと配置マニフェストに再署名する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fc69ce1f79644d7f4b35fbb1c1e3a41691761390
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81649183"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストおよび配置マニフェストに再署名する
Windows フォーム アプリケーション、Windows プレゼンテーション基盤アプリケーション (xbap)、または Office ソリューションのアプリケーション マニフェストで配置プロパティを変更した後、アプリケーション マニフェストと配置マニフェストの両方に証明書を使用して再署名する必要があります。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。

 マニフェストに再署名する別のシナリオとして、ユーザーがアプリケーション マニフェストと配置マニフェストに独自の証明書を使用して署名する場合があります。

## <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名
 この手順は、アプリケーション マニフェスト ファイル (*.manifest*) に既に変更を加えたものと仮定します。 詳細については、「[方法 : 展開プロパティを変更する](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472)」を参照してください。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーション マニフェストと配置マニフェストに再署名するには

1. Visual **Studio コマンド プロンプト**ウィンドウを開きます。

2. ディレクトリを、署名するマニフェスト ファイルが格納されているフォルダーに変更します。

3. 次のコマンドを入力して、アプリケーション マニフェスト ファイルに署名します。 *マニフェスト ファイル名*を、マニフェスト ファイルの名前と拡張子に置き換えます。 *証明書を証明書*ファイルの相対パスまたは完全修飾パスに置き換え *、Password*を証明書のパスワードに置き換えます。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォーム アプリケーション、または Windows プレゼンテーション ファンデーション ブラウザー アプリケーションのアプリケーション マニフェストに署名するには、次のコマンドを実行します。 Visual Studio によって作成された一時的な証明書は、運用環境への配置には推奨されません。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 次のコマンドを入力して、配置マニフェスト ファイルを更新して署名し、前の手順と同じプレースホルダ名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォーム アプリケーション、または Windows プレゼンテーション ファンデーション ブラウザー アプリケーションの配置マニフェストを更新して署名できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 必要に応じて、マスター配置マニフェスト *(\\\<appname>.application*) をバージョン配置ディレクトリ (*publish\Application\\\<Files アプリ名>_ バージョン>\< *) にコピーします。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストを更新して再署名する
 この手順では、アプリケーション マニフェスト ファイル (*.manifest*) に既に変更を加えたが、更新されたファイルが他に存在することを前提としています。 ファイルが更新されると、ファイルを表すハッシュも更新する必要があります。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーション マニフェストと配置マニフェストを更新し、再署名するには

1. Visual **Studio コマンド プロンプト**ウィンドウを開きます。

2. ディレクトリを、署名するマニフェスト ファイルが格納されているフォルダーに変更します。

3. 発行出力フォルダー内のファイルから *.deploy*ファイル拡張子を削除します。

4. 次のコマンドを入力して、更新されたファイルの新しいファイルの新しいコードでアプリケーション マニフェストを更新し、アプリケーション マニフェスト ファイルに署名します。 *マニフェスト ファイル名*を、マニフェスト ファイルの名前と拡張子に置き換えます。 *証明書を証明書*ファイルの相対パスまたは完全修飾パスに置き換え *、Password*を証明書のパスワードに置き換えます。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォーム アプリケーション、または Windows プレゼンテーション ファンデーション ブラウザー アプリケーションのアプリケーション マニフェストに署名するには、次のコマンドを実行します。 Visual Studio によって作成された一時的な証明書は、運用環境への配置には推奨されません。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 次のコマンドを入力して、配置マニフェスト ファイルを更新して署名し、前の手順と同じプレースホルダ名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォーム アプリケーション、または Windows プレゼンテーション ファンデーション ブラウザー アプリケーションの配置マニフェストを更新して署名できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. アプリケーション マニフェスト ファイルと配置マニフェスト ファイルを除き *、.deploy*ファイル拡張子をファイルに追加します。

7. 必要に応じて、マスター配置マニフェスト *(\\\<appname>.application*) をバージョン配置ディレクトリ (*publish\Application\\\<Files アプリ名>_ バージョン>\< *) にコピーします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法 : ClickOnce アプリケーションのセキュリティ ゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)