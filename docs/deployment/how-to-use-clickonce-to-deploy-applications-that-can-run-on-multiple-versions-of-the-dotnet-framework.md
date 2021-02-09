---
title: ClickOnce を使用してマルチターゲットアプリをデプロイする
description: ClickOnce 配置テクノロジを使用して、複数のバージョンの .NET Framework を対象とするアプリケーションを配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, multiple .NET Framework versions
- ClickOnce deployment, multiple .NET Framework versions
- deploying applications [ClickOnce], multiple .NET Framework versions
ms.assetid: e0a8c330-21bc-4eb2-b936-fd0f3c3221f1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: c87ed73d2c3a26ecc4522c6497ac71e33e46a6c3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889123"
---
# <a name="how-to-use-clickonce-to-deploy-applications-that-can-run-on-multiple-versions-of-the-net-framework"></a>方法: ClickOnce を使用して、複数のバージョンの .NET Framework で実行できるアプリケーションを配置する
ClickOnce 配置テクノロジを使用して、複数のバージョンの .NET Framework を対象とするアプリケーションを配置できます。 そのためには、アプリケーションマニフェストと配置マニフェストを生成して更新する必要があります。

> [!NOTE]
> 複数のバージョンの .NET Framework を対象とするようにアプリケーションを変更する前に、アプリケーションが複数のバージョンの .NET Framework で実行されていることを確認する必要があります。 共通言語ランタイムのバージョンは、.NET Framework 4、.NET Framework 2.0、.NET Framework 3.0、および .NET Framework 3.5 とは異なります。

 このプロセスには、次の手順が必要です。

1. アプリケーションマニフェストと配置マニフェストを生成します。

2. 複数の .NET Framework バージョンを一覧表示するように配置マニフェストを変更します。

3. 互換性のある .NET Framework ランタイムバージョンを一覧表示するように *app.config* ファイルを変更します。

4. 依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーションマニフェストを変更します。

5. アプリケーションマニフェストに署名します。

6. デプロイマニフェストを更新して署名します。

### <a name="to-generate-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストを生成するには

- プロジェクトデザイナーの発行ウィザードまたは [発行] ページを使用して、アプリケーションを発行し、アプリケーションマニフェストと配置マニフェストファイルを生成します。 詳細については、「方法: 発行ウィザードまたは [[発行] ページ (プロジェクトデザイナー)](../ide/reference/publish-page-project-designer.md)[を使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。

### <a name="to-change-the-deployment-manifest-to-list-the-multiple-net-framework-versions"></a>複数の .NET Framework バージョンを一覧表示するように配置マニフェストを変更するには

1. 発行ディレクトリで、Visual Studio の XML エディターを使用して配置マニフェストを開きます。 配置マニフェストには、 *アプリケーション* のファイル名拡張子が付いています。

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

1. ソリューションエクスプローラーで、Visual Studio の XML エディターを使用して、 *app.config* ファイルを開きます。

2. 要素と要素の間の XML コードを、 `<startup>` `</startup>` アプリケーションでサポートされている .NET Framework ランタイムの一覧を示す xml に置き換えます (または追加します)。

     次の表は、使用可能な .NET Framework バージョンの一部と、配置マニフェストに追加できる対応する XML を示しています。

    |.NET Framework ランタイムバージョン|XML|
    |------------------------------------|---------|
    |4 Client|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0,Profile=Client" />|
    |4 Full|\<supportedRuntime version="v4.0.30319" sku=".NETFramework,Version=v4.0" />|
    |3.5 Full|\<supportedRuntime version="v2.0.50727"/>|
    |3.5 Client|\<supportedRuntime version="v2.0.50727" sku="Client"/>|

### <a name="to-change-the-application-manifest-to-mark-dependent-assemblies-as-net-framework-assemblies"></a>依存アセンブリを .NET Framework アセンブリとしてマークするようにアプリケーションマニフェストを変更するには

1. 発行ディレクトリで、Visual Studio の XML エディターを使用して、アプリケーションマニフェストを開きます。 配置マニフェストには、 *.manifest* というファイル名拡張子が付いています。

2. `group="framework"`Sentinel アセンブリ ( `System.Core` 、、 `WindowsBase` `Sentinel.v3.5Client` 、および) の dependency XML にを追加し `System.Data.Entity` ます。 たとえば、XML は次のようになります。

   ```xml
   <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" group="framework">
   ```

3. CommonLanguageRuntime の要素のバージョン番号 `<assemblyIdentity>` を、最も一般的な分母である .NET Framework のバージョン番号に更新します。 たとえば、アプリケーションが3.5 および .NET Framework 4 .NET Framework 対象である場合は、2.0.50727.0 バージョン番号を使用します。 XML は次のようになります。

   ```xml
   <dependency>
     <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">
       <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50727.0" />
     </dependentAssembly>
   </dependency>
   ```

### <a name="to-update-and-re-sign-the-application-and-deployment-manifests"></a>アプリケーションマニフェストと配置マニフェストを更新して再署名するには

- アプリケーションマニフェストと配置マニフェストを更新し、再署名します。 詳細については、「 [方法: アプリケーションマニフェストおよび配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [\<compatibleFrameworks> 要素](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [\<dependency> 要素](../deployment/dependency-element-clickonce-application.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [構成ファイル スキーマ](/dotnet/framework/configure-apps/file-schema/index)
