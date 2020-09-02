---
title: '方法: アプリケーションマニフェストと配置マニフェストに再署名するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d5956ad23fe22c7c36b712fac61df268586142df
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697557"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストおよび配置マニフェストに再署名する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows フォームアプリケーション、Windows Presentation Foundation アプリケーション (xbap)、または Office ソリューションのアプリケーションマニフェストの配置プロパティを変更した後、アプリケーションマニフェストと配置マニフェストの両方に証明書を使用して再署名する必要があります。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。  
  
 マニフェストに再署名できるもう1つのシナリオは、顧客が独自の証明書を使用してアプリケーションマニフェストと配置マニフェストに署名する場合です。  
  
## <a name="re-signing-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストに再署名する  
 この手順では、既にアプリケーションマニフェストファイル (.manifest) に変更を加えていることを前提としています。 詳細については、「 [方法: 配置プロパティを変更する](https://msdn.microsoft.com/66052a3a-8127-4964-8147-2477ef5d1472)」を参照してください。  
  
#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーションマニフェストと配置マニフェストに再署名するには  
  
1. **Visual Studio のコマンドプロンプト**ウィンドウを開きます。  
  
2. 署名するマニフェストファイルが格納されているフォルダーにディレクトリを変更します。  
  
3. 次のコマンドを入力して、アプリケーションマニフェストファイルに署名します。 ManifestFileName は、マニフェストファイルの名前と拡張子を加えたものに置き換えます。 証明書を証明書ファイルの相対パスまたは完全修飾パスに置き換え、Password を証明書のパスワードに置き換えます。  
  
    ```  
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     たとえば、アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションのアプリケーションマニフェストに署名するには、次のコマンドを実行します。 実稼働環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。  
  
    ```  
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
4. 次のコマンドを入力して、配置マニフェストファイルを更新して署名します。これには、前の手順で示したプレースホルダー名を置き換えます。  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションの配置マニフェストを更新し、署名することができます。  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5. 必要に応じて、マスター配置マニフェスト ( \\ *appname appname*. application) をバージョン配置ディレクトリ (publish\Application Files \\ *appname*_*バージョン*) にコピーします。  
  
## <a name="updating-and-re-signing-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストの更新と再署名  
 この手順では、既にアプリケーションマニフェストファイル (.manifest) を変更したが、更新された他のファイルがあることを前提としています。 ファイルが更新された場合は、ファイルを表すハッシュも更新する必要があります。  
  
#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してアプリケーションマニフェストと配置マニフェストを更新して再署名するには  
  
1. **Visual Studio のコマンドプロンプト**ウィンドウを開きます。  
  
2. 署名するマニフェストファイルが格納されているフォルダーにディレクトリを変更します。  
  
3. 発行出力フォルダー内のファイルから .deploy ファイル拡張子を削除します。  
  
4. 次のコマンドを入力して、更新されたファイルの新しいハッシュでアプリケーションマニフェストを更新し、アプリケーションマニフェストファイルに署名します。 ManifestFileName は、マニフェストファイルの名前と拡張子を加えたものに置き換えます。 証明書を証明書ファイルの相対パスまたは完全修飾パスに置き換え、Password を証明書のパスワードに置き換えます。  
  
    ```  
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password  
    ```  
  
     たとえば、アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションのアプリケーションマニフェストに署名するには、次のコマンドを実行します。 実稼働環境への配置では、Visual Studio によって作成された一時的な証明書は推奨されません。  
  
    ```  
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
5. 次のコマンドを入力して、配置マニフェストファイルを更新して署名します。これには、前の手順で示したプレースホルダー名を置き換えます。  
  
    ```  
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password  
    ```  
  
     たとえば、次のコマンドを実行して、Excel アドイン、Windows フォームアプリケーション、または Windows Presentation Foundation ブラウザーアプリケーションの配置マニフェストを更新し、署名することができます。  
  
    ```  
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx  
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx  
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx  
    ```  
  
6. アプリケーションマニフェストファイルと配置マニフェストファイルを除き、.deploy ファイル拡張子をファイルに戻します。  
  
7. 必要に応じて、マスター配置マニフェスト ( \\ *appname appname*. application) をバージョン配置ディレクトリ (publish\Application Files \\ *appname*_*バージョン*) にコピーします。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)   
 [ClickOnce アプリケーションのコードアクセスセキュリティ](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)   
 [信頼されたアプリケーションの展開の概要](../deployment/trusted-application-deployment-overview.md)   
 [方法: ClickOnce のセキュリティ設定を有効にする](../deployment/how-to-enable-clickonce-security-settings.md)   
 [方法: ClickOnce アプリケーションのセキュリティゾーンを設定する](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [方法: ClickOnce アプリケーション用の信頼された発行者をクライアントコンピューターに追加する](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)
