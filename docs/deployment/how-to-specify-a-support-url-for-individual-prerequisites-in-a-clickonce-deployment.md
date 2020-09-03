---
title: ClickOnce 配置の前提条件のサポート URL
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf474e4926403a9475860bfdc620ee4a6860f8aa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85381731"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>方法: ClickOnce 配置で個々の必要条件にサポート URL を指定する
展開では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを実行するためにクライアントコンピューターで使用できる必要があるいくつかの前提条件をテストでき [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 これらの依存関係には、必要な最小バージョンの .NET Framework、オペレーティングシステムのバージョン、およびグローバルアセンブリキャッシュ (GAC) にプレインストールする必要があるすべてのアセンブリが含まれます。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]ただし、これらの必須コンポーネントをインストールすることはできません。前提条件が見つからない場合は、インストールを停止するだけで、インストールが失敗した原因を説明するダイアログボックスが表示されます。

 必須コンポーネントをインストールする方法は2つあります。 ブートストラップアプリケーションを使用してインストールできます。 または、前提条件が見つからない場合に、ダイアログボックスでユーザーに表示される個々の必須コンポーネントのサポート URL を指定することもできます。 この URL によって参照されるページには、必要な前提条件をインストールするための手順へのリンクを含めることができます。 アプリケーションで個々の前提条件のサポート URL が指定されていない場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションが定義されていれば、そのアプリケーション全体の配置マニフェストで指定されているサポート url がに表示されます。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、 *Mage.exe*、 *MageUI.exe*すべてを使用して展開を生成できますが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、これらのツールでは、個々の前提条件のサポート URL を直接指定することはできません。 このドキュメントでは、配置のアプリケーションマニフェストと配置マニフェストを変更して、これらのサポート Url を含める方法について説明します。

### <a name="specify-a-support-url-for-an-individual-prerequisite"></a>個々の前提条件のサポート URL を指定する

1. アプリケーションのアプリケーションマニフェスト ( *.manifest* ファイル) を [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テキストエディターで開きます。

2. オペレーティングシステムの前提条件として、 `supportUrl` 属性を要素に追加し `dependentOS` ます。

   ```xml
    <dependency>
       <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">
         <osVersionInfo>
           <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />
         </osVersionInfo>
       </dependentOS>
     </dependency>
   ```

3. 共通言語ランタイムの特定のバージョンの前提条件については、 `supportUrl` `dependentAssembly` 共通言語ランタイムの依存関係を指定するエントリに属性を追加します。

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">
         <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />
       </dependentAssembly>
     </dependency>
   ```

4. グローバルアセンブリキャッシュにプレインストールする必要があるアセンブリの前提条件については、 `supportUrl` `dependentAssembly` 必要なアセンブリを指定する要素のをに設定します。

   ```xml
     <dependency>
       <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">
         <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />
       </dependentAssembly>
     </dependency>
   ```

5. 省略可能。 .NET Framework 4 を対象とするアプリケーションでは、アプリケーションの配置マニフェスト ( *アプリケーション* ファイル) を [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] テキストエディターで開きます。

6. .NET Framework 4 の前提条件として、 `supportUrl` 属性を要素に追加し `compatibleFrameworks` ます。

   ```xml
   <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">
     <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />
     <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />
   </compatibleFrameworks>
   ```

7. アプリケーションマニフェストを手動で変更したら、デジタル証明書を使用してアプリケーションマニフェストに再署名してから、配置マニフェストも更新して再署名する必要があります。 このタスクを実行するには、 *Mage.exe* または *MageUI.exe* SDK ツールを使用します。手動による変更を消去して、これらのファイルを再生成することも [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] できます。 Mage.exe を使用したマニフェストの再署名の詳細については、「 [方法: アプリケーションマニフェストと配置マニフェストに再署名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)する」を参照してください。

## <a name="net-framework-security"></a>.NET Framework のセキュリティ
 アプリケーションが部分信頼で実行するようにマークされている場合、このサポート URL はダイアログボックスに表示されません。

## <a name="see-also"></a>関連項目
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [\<compatibleFrameworks> element](../deployment/compatibleframeworks-element-clickonce-deployment.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)