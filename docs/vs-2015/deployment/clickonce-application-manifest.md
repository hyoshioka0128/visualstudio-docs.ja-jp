---
title: ClickOnce アプリケーションマニフェスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- application manifests [ClickOnce]
- ClickOnce, application manifests
ms.assetid: 29570cec-4e53-4660-a850-abc4fa150243
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: adf5e160ec334859062311fae947ce34e79850d5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157425"
---
# <a name="clickonce-application-manifest"></a>ClickOnce Application Manifest
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションマニフェストは、を使用して配置されるアプリケーションを記述する XML ファイルです [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションマニフェストには、次の要素と属性があります。  
  
|要素|説明|属性|  
|-------------|-----------------|----------------|  
|[\<assembly> 要素](../deployment/assembly-element-clickonce-application.md)|必須です。 最上位の要素です。|`manifestVersion`|  
|[\<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)|必須です。 アプリケーションのプライマリアセンブリを識別し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。|`name`<br /><br /> `version`<br /><br /> `publicKeyToken`<br /><br /> `processorArchitecture`<br /><br /> `language`|  
|[\<trustInfo> 要素](../deployment/trustinfo-element-clickonce-application.md)|アプリケーションのセキュリティ要件を識別します。|なし|  
|[\<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)|必須です。 アプリケーションコードのエントリポイントを識別します。|`name`|  
|[\<dependency> 要素](../deployment/dependency-element-clickonce-application.md)|必須です。 アプリケーションを実行するために必要な依存関係をそれぞれ識別します。 任意で、プレインストールする必要のあるアセンブリを識別します。|なし|  
|[\<file> 要素](../deployment/file-element-clickonce-application.md)|省略可能。 アプリケーションによって使用されるアセンブリ以外の各ファイルを識別します。 ファイルに関連付けられているコンポーネント オブジェクト モデル (COM) 分離データを含めることができます。|`name`<br /><br /> `size`<br /><br /> `group`<br /><br /> `optional`<br /><br /> `writeableType`|  
|[\<fileAssociation> 要素](../deployment/fileassociation-element-clickonce-application.md)|省略可能。 アプリケーションに関連付けるファイル拡張子を識別します。|`extension`<br /><br /> `description`<br /><br /> `progid`<br /><br /> `defaultIcon`|  
  
## <a name="remarks"></a>注釈  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションマニフェストファイルは、を使用して展開されたアプリケーションを識別し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] の詳細については、「[ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)」を参照してください。  
  
## <a name="file-location"></a>ファイルの場所  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションマニフェストは、デプロイの1つのバージョンに固有です。 このため、配置マニフェストとは別に保存する必要があります。 一般的な規則では、関連付けられたバージョンの後に名前が付けられたサブディレクトリに配置されます。  
  
 アプリケーションマニフェストは、展開する前に常に署名されている必要があります。 アプリケーションマニフェストを手動で変更した場合は、mage.exe を使用してアプリケーションマニフェストに再署名し、配置マニフェストを更新してから、配置マニフェストに再署名する必要があります。 詳細については、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」を参照してください。  
  
## <a name="file-name-syntax"></a>ファイル名の構文  
 アプリケーションマニフェストファイルの名前は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 要素で識別されるアプリケーションの完全な名前と拡張子、および `assemblyIdentity` 拡張子 .manifest を持つ必要があります。 たとえば、Example.exe アプリケーションを参照するアプリケーションマニフェストでは、次のファイル名構文を使用します。  
  
 `example.exe.manifest`  
  
## <a name="example"></a>例  
 次のコード例は、アプリケーションのアプリケーションマニフェストを示して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] います。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<asmv1:assembly xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd" manifestVersion="1.0" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2" xmlns="urn:schemas-microsoft-com:asm.v2" xmlns:asmv1="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">  
  <asmv1:assemblyIdentity name="My Application Deployment.exe" version="1.0.0.0" publicKeyToken="43cb1e8e7a352766" language="neutral" processorArchitecture="x86" type="win32" />  
  <application />  
  <entryPoint>  
    <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />  
    <commandLine file="MyApplication.exe" parameters="" />  
  </entryPoint>  
  <trustInfo>  
    <security>  
      <applicationRequestMinimum>  
        <PermissionSet Unrestricted="true" ID="Custom" SameSite="site" />  
        <defaultAssemblyRequest permissionSetReference="Custom" />  
      </applicationRequestMinimum>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <!--  
          UAC Manifest Options  
          If you want to change the Windows User Account Control level replace the   
          requestedExecutionLevel node with one of the following.  
  
        <requestedExecutionLevel  level="asInvoker" uiAccess="false" />  
        <requestedExecutionLevel  level="requireAdministrator" uiAccess="false" />  
        <requestedExecutionLevel  level="highestAvailable" uiAccess="false" />  
  
         If you want to utilize File and Registry Virtualization for backward   
         compatibility then delete the requestedExecutionLevel node.  
    -->  
        <requestedExecutionLevel level="asInvoker" uiAccess="false" />  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
  <dependency>  
    <dependentOS>  
      <osVersionInfo>  
        <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
      </osVersionInfo>  
    </dependentOS>  
  </dependency>  
  <dependency>  
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
      <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.20506.0" />  
    </dependentAssembly>  
  </dependency>  
  <dependency>  
    <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="4096">  
      <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />  
      <hash>  
        <dsig:Transforms>  
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
        </dsig:Transforms>  
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
        <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>  
      </hash>  
    </dependentAssembly>  
  </dependency>  
<publisherIdentity name="CN=DOMAINCONTROLLER\UserMe" issuerKeyHash="18312a18a21b215ecf4cdb20f5a0e0b0dd263c08" /><Signature Id="StrongNameSignature" xmlns="http://www.w3.org/2000/09/xmldsig#">  
…  
</Signature></r:issuer></r:license></msrel:RelData></KeyInfo></Signature></asmv1:assembly>  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
