---
title: '&lt;entryPoint &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#commandLine
- urn:schemas-microsoft-com:asm.v2#entryPoint
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <entryPoint> element [ClickOnce application manifest]
- manifests [ClickOnce], entryPoint element
ms.assetid: 10ad3083-10c1-4189-a870-9bba2eab244f
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9ce9fcbddf54dff0ee8574d0c2a5a3df4d8b5c7e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193507"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;entryPoint &gt; 要素 (ClickOnce アプリケーション)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションがクライアントコンピューターで実行されるときに実行する必要があるアセンブリを識別します。  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      <entryPoint  
   name  
>  
   <assemblyIdentity  
      name  
      version  
      processorArchitecture  
      language  
   />  
   <commandLine  
      file  
      parameters  
   />  
   <customHostRequired />  
   <customUX />  
</entryPoint>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 `entryPoint` 要素は必須です。この要素は `urn:schemas-microsoft-com:asm.v2` 名前空間にあります。 `entryPoint`アプリケーションマニフェストで定義されている要素は1つだけです。  
  
 `entryPoint` 要素には、次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`name`|省略可能。 この値は .NET Framework では使用されません。|  
  
 `entryPoint` には、次の要素があります。  
  
## <a name="assemblyidentity"></a>assemblyIdentity  
 必須です。 とその属性の役割は、 `assemblyIdentity` [ \<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)で定義されています。  
  
 `processorArchitecture`この要素の属性と、 `processorArchitecture` アプリケーションマニフェスト内の他の場所で定義されている属性が一致している `assemblyIdentity` 必要があります。  
  
## <a name="commandline"></a>commandLine  
 必須です。 要素の子である必要があり `entryPoint` ます。 子要素はなく、次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`file`|必須です。 アプリケーションのスタートアップアセンブリへのローカル参照 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 。 この値には、スラッシュ (/) または円記号 () のパス区切り文字を含めることはできません \\ 。|  
|`parameters`|必須です。 エントリポイントで実行するアクションについて説明します。 有効な値はのみです。 `run` 空の文字列を指定すると、 `run` が想定されます。|  
  
## <a name="customhostrequired"></a>customHostRequired  
 省略可能。 含まれている場合、この展開には、カスタムホスト内に展開され、スタンドアロンアプリケーションではないコンポーネントが含まれていることを指定します。  
  
 この要素が存在する場合は `assemblyIdentity` 、 `commandLine` 要素と要素も存在していなければなりません。 存在する場合は、の [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] インストール中に検証エラーが発生します。  
  
 この要素には属性がなく、子もありません。  
  
## <a name="customux"></a>customUX  
 省略可能。 アプリケーションがカスタムインストーラーによってインストールおよび管理され、[スタート] メニューのエントリ、ショートカット、または [プログラムの追加と削除] エントリが作成されないことを指定します。  
  
```  
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />  
```  
  
 CustomUX 要素を含むアプリケーションは、 <xref:System.Deployment.Application.InPlaceHostingManager> インストール操作を実行するためにクラスを使用するカスタムインストーラーを提供する必要があります。 この要素を含むアプリケーションは、マニフェストをダブルクリックするか、前提条件のブートストラップを setup.exe してインストールすることはできません。 カスタムインストーラーでは、[スタート] メニューのエントリ、ショートカット、および [プログラムの追加と削除] エントリを作成できます。 カスタムインストーラーで [プログラムの追加と削除] エントリが作成されない場合は、プロパティによって提供されるサブスクリプション識別子を格納 <xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> し、ユーザーがメソッドを呼び出して後でアプリケーションをアンインストールできるようにする必要があり <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> ます。 詳細については、「 [チュートリアル: ClickOnce アプリケーションのカスタムインストーラーを作成](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)する」を参照してください。  
  
## <a name="remarks"></a>注釈  
 この要素は、アプリケーションのアセンブリとエントリポイントを識別し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
 を使用し `commandLine` て、実行時にアプリケーションにパラメーターを渡すことはできません。 アプリケーションのからデプロイのクエリ文字列パラメーターにアクセスでき [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] <xref:System.AppDomain> ます。 詳細については、「 [方法: オンライン ClickOnce アプリケーションでクエリ文字列情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、アプリケーションマニフェストの要素を示してい `entryPoint` [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 このコード例は、 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md) トピック用に用意されている、より大きな例の一部です。  
  
```  
<!-- Identify the main code entrypoint. -->  
<!-- This code runs the main method in an executable assembly. -->  
  <entryPoint>  
    <assemblyIdentity   
      name="MyApplication"   
      version="1.0.0.0"  
      language="neutral"  
      processorArchitecture="x86" />  
    <commandLine file="MyApplication.exe" parameters="" />  
  </entryPoint>  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
