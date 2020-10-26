---
title: '方法: ClickOnce を使用して、複数のバージョンの .NET Framework で実行できるアプリケーションを配置するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 164fe64f360e41c06ef3f7bfd2d8091a6ebefecd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65679946"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>方法: ClickOnce を使用して、複数のバージョンの .NET Framework で実行できるアプリケーションを配置する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ClickOnce 配置テクノロジを使用して、複数のバージョンの .NET Framework を対象とするアプリケーションを配置できます。 そのためには、アプリケーションマニフェストと配置マニフェストを生成して更新する必要があります。  
  
> [!NOTE]
> 複数のバージョンの .NET Framework を対象とするようにアプリケーションを変更する前に、アプリケーションが複数のバージョンの .NET Framework で実行されていることを確認する必要があります。 共通言語ランタイムのバージョンは、 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] .NET Framework 2.0、.NET Framework 3.0、.NET Framework 3.5 とは異なります。  
  
 このプロセスには、次の手順が必要です。  
  
1. アプリケーションマニフェストと配置マニフェストを生成します。  
  
2. 複数の .NET Framework バージョンを一覧表示するように配置マニフェストを変更します。  
  
3. 互換性のある .NET Framework ランタイムバージョンを一覧表示するように app.config ファイルを変更します。  
  
4. 依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーションマニフェストを変更します。  
  
5. アプリケーションマニフェストに署名します。  
  
6. デプロイマニフェストを更新して署名します。  
  
### <a name="to-generate-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストを生成するには  
  
- プロジェクトデザイナーの発行ウィザードまたは [発行] ページを使用して、アプリケーションを発行し、アプリケーションマニフェストと配置マニフェストファイルを生成します。 詳細については、「方法: 発行ウィザードまたは [[発行] ページ (プロジェクトデザイナー)](../ide/reference/publish-page-project-designer.md)[を使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。  
  
### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>複数の .NET Framework バージョンを一覧表示するように配置マニフェストを変更するには  
  
1. 発行ディレクトリで、Visual Studio の XML エディターを使用して配置マニフェストを開きます。 配置マニフェストには、アプリケーションのファイル名拡張子が付いています。  
  
2. 要素と要素の間の XML コードを、 `<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">` `</compatibleFrameworks>` アプリケーションでサポートされている .NET Framework バージョンを示す xml に置き換えます。  
  
     次の表は、使用可能な .NET Framework バージョンの一部と、配置マニフェストに追加できる対応する XML を示しています。  
  
    |.NET Framework のバージョン|XML|  
    |----------------------------|---------|  
    |4 Client|\<framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />|  
    |4 Full|\<framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />|  
    |3.5 Client|\<framework targetVersion="3.5" profile="Client" supportedRuntime="2.0.50727" />|  
    |3.5 Full|\<framework targetVersion="3.5" profile="Full" supportedRuntime="2.0.50727" />|  
    |3.0|\<framework targetVersion="3.0" supportedRuntime="2.0.50727" />|  
  
### <a name="to-change-the-appconfig-file-to-list-the-compatible-net-framework-runtime-versions"></a>互換性のある .NET Framework ランタイムバージョンを一覧表示するように app.config ファイルを変更するには  
  
1. ソリューションエクスプローラーで、Visual Studio の XML エディターを使用して、App.config ファイルを開きます。  
  
2. 要素と要素の間の XML コードを、 `<startup>` `</startup>` アプリケーションでサポートされている .NET Framework ランタイムの一覧を示す xml に置き換えます (または追加します)。  
  
     次の表は、使用可能な .NET Framework バージョンの一部と、配置マニフェストに追加できる対応する XML を示しています。  
  
    |.NET Framework ランタイムバージョン|XML|  
    |------------------------------------|---------|  
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|  
    |4 Full|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|  
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|  
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|  
  
### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーションマニフェストを変更するには  
  
1. 発行ディレクトリで、Visual Studio の XML エディターを使用して、アプリケーションマニフェストを開きます。 配置マニフェストには、.manifest というファイル名拡張子が付いています。  
  
2. `group="framework"`Sentinel アセンブリ ( `System.Core` 、、 `WindowsBase` `Sentinel.v3.5Client` 、および) の dependency XML にを追加し `System.Data.Entity` ます。 たとえば、XML は次のようになります。  
  
    ```  
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">  
    ```  
  
3. CommonLanguageRuntime の要素のバージョン番号 `<assemblyIdentity>` を、最も一般的な分母である .NET Framework のバージョン番号に更新します。 たとえば、アプリケーションの対象が3.5 で .NET Framework、 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 2.0.50727.0 のバージョン番号を使用している場合、XML は次のようになります。  
  
    ```  
    <dependency>  
      <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
        <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />  
      </dependentAssembly>  
    </dependency>  
    ```  
  
### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストを更新して再署名するには  
  
- アプリケーションマニフェストと配置マニフェストを更新し、再署名します。 詳細については、「 [How to: Re-sign Application and Deployment Manifests](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [\<compatibleFrameworks> Element](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [\<dependency> Element](../deployment/dependency-element-clickonce-application.md)   
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)   
 [構成ファイル スキーマ](https://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38)
