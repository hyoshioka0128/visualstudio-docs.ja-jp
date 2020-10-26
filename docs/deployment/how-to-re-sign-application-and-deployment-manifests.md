---
title: アプリケーションマニフェストと配置マニフェストに再署名する方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
ms.openlocfilehash: 9c8c76a789ac4a50e1128dc0897b9a08a185117a
ms.sourcegitcommit: 1803a67b516f67b209d8f4cf147314e604ef1927
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641599"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストおよび配置マニフェストに再署名する
Windows フォームアプリケーション、Windows Presentation Foundation アプリケーション (xbap)、または Office ソリューションのアプリケーションマニフェストの配置プロパティを変更した後、アプリケーションマニフェストと配置マニフェストの両方に証明書を使用して再署名する必要があります。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。

 マニフェストに再署名できるもう1つのシナリオは、顧客が独自の証明書を使用してアプリケーションマニフェストと配置マニフェストに署名する場合です。

## <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名
 この手順では、既にアプリケーションマニフェストファイル (*.manifest*) に変更を加えていることを前提としています。 詳細については、「 [方法: 配置プロパティを変更する](/previous-versions/cc442869(v=vs.110))」を参照してください。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーションマニフェストと配置マニフェストに再署名するには

1. **Visual Studio のコマンドプロンプト**ウィンドウを開きます。

2. 署名するマニフェストファイルが格納されているフォルダーにディレクトリを変更します。

3. 次のコマンドを入力して、アプリケーションマニフェストファイルに署名します。 *Manifestfilename*は、マニフェストファイルの名前と拡張子を加えたものに置き換えます。 証明書を証明書ファイルの相対パスまたは完全修飾パス *に置き換え、* *password* を証明書のパスワードに置き換えます。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションのアプリケーションマニフェストに署名するには、次のコマンドを実行します。 実稼働環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 次のコマンドを入力して、配置マニフェストファイルを更新して署名します。これには、前の手順で示したプレースホルダー名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションの配置マニフェストを更新し、署名することができます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 必要に応じて、マスター配置マニフェスト (*publish \\ \<appname> . application*) をバージョン配置ディレクトリ (*publish\Application Files \\ \<appname> _ \<version> *) にコピーします。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストを更新して再署名する
 この手順では、既にアプリケーションマニフェストファイル (*.manifest*) を変更したが、更新された他のファイルがあることを前提としています。 ファイルが更新された場合は、ファイルを表すハッシュも更新する必要があります。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーションマニフェストと配置マニフェストを更新して再署名するには

1. **Visual Studio のコマンドプロンプト**ウィンドウを開きます。

2. 署名するマニフェストファイルが格納されているフォルダーにディレクトリを変更します。

3. 発行出力フォルダー内のファイルから *.deploy* ファイル拡張子を削除します。

4. 次のコマンドを入力して、更新されたファイルの新しいハッシュでアプリケーションマニフェストを更新し、アプリケーションマニフェストファイルに署名します。 *Manifestfilename*は、マニフェストファイルの名前と拡張子を加えたものに置き換えます。 証明書を証明書ファイルの相対パスまたは完全修飾パス *に置き換え、* *password* を証明書のパスワードに置き換えます。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションのアプリケーションマニフェストに署名するには、次のコマンドを実行します。 実稼働環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 次のコマンドを入力して、配置マニフェストファイルを更新して署名します。これには、前の手順で示したプレースホルダー名を置き換えます。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションの配置マニフェストを更新し、署名することができます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. アプリケーションマニフェストファイルと配置マニフェストファイルを除き、.deploy ファイル拡張子をファイルに戻し*ます。*

7. 必要に応じて、マスター配置マニフェスト (*publish \\ \<appname> . application*) をバージョン配置ディレクトリ (*publish\Application Files \\ \<appname> _ \<version> *) にコピーします。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](securing-clickonce-applications.md)
- [方法: ClickOnce アプリケーション用の信頼された発行者をクライアント コンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)