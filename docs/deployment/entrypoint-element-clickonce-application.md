---
title: '&lt;entryPoint &gt; 要素 (ClickOnce アプリケーション) |Microsoft Docs'
description: EntryPoint 要素は、この ClickOnce アプリケーションがクライアントコンピューターで実行されるときに実行する必要があるアセンブリを識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d5c35d94001ae1e883e2bd76650f248d7e0364d2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893894"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;entryPoint &gt; 要素 (ClickOnce アプリケーション)
この [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションがクライアントコンピューターで実行されるときに実行する必要があるアセンブリを識別します。

## <a name="syntax"></a>構文

```xml
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
|`name`|任意。 この値は .NET Framework では使用されません。|

 `entryPoint` には、次の要素があります。

## <a name="assemblyidentity"></a>assemblyIdentity
 必須。 とその属性の役割は、 `assemblyIdentity` [ \<assemblyIdentity> 要素](../deployment/assemblyidentity-element-clickonce-application.md)で定義されています。

 `processorArchitecture`この要素の属性と、 `processorArchitecture` アプリケーションマニフェスト内の他の場所で定義されている属性が一致している `assemblyIdentity` 必要があります。

## <a name="commandline"></a>commandLine
 必須。 要素の子である必要があり `entryPoint` ます。 子要素はなく、次の属性があります。

| 属性 | 説明 |
|--------------| - |
| `file` | 必須。 アプリケーションのスタートアップアセンブリへのローカル参照 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 この値には、スラッシュ (/) または円記号 () のパス区切り文字を含めることはできません \\ 。 |
| `parameters` | 必須。 エントリポイントで実行するアクションについて説明します。 有効な値はのみです。 `run` 空の文字列を指定すると、 `run` が想定されます。 |

## <a name="customhostrequired"></a>customHostRequired
 任意。 含まれている場合、この展開には、カスタムホスト内に展開され、スタンドアロンアプリケーションではないコンポーネントが含まれていることを指定します。

 この要素が存在する場合は `assemblyIdentity` 、 `commandLine` 要素と要素も存在していなければなりません。 存在する場合は、の [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] インストール中に検証エラーが発生します。

 この要素には属性がなく、子もありません。

## <a name="customux"></a>customUX
 任意。 アプリケーションがカスタムインストーラーによってインストールおよび管理され、[スタート] メニューのエントリ、ショートカット、または [プログラムの追加と削除] エントリが作成されないことを指定します。

```xml
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />
```

 CustomUX 要素を含むアプリケーションは、 <xref:System.Deployment.Application.InPlaceHostingManager> インストール操作を実行するためにクラスを使用するカスタムインストーラーを提供する必要があります。 この要素を含むアプリケーションは、マニフェストをダブルクリックするか、前提条件のブートストラップを setup.exe してインストールすることはできません。 カスタムインストーラーでは、[スタート] メニューのエントリ、ショートカット、および [プログラムの追加と削除] エントリを作成できます。 カスタムインストーラーで [プログラムの追加と削除] エントリが作成されない場合は、プロパティによって提供されるサブスクリプション識別子を格納 <xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> し、ユーザーがメソッドを呼び出して後でアプリケーションをアンインストールできるようにする必要があり <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> ます。 詳細については、「 [チュートリアル: ClickOnce アプリケーションのカスタムインストーラーを作成](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)する」を参照してください。

## <a name="remarks"></a>解説
 この要素は、アプリケーションのアセンブリとエントリポイントを識別し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

 を使用し `commandLine` て、実行時にアプリケーションにパラメーターを渡すことはできません。 アプリケーションのからデプロイのクエリ文字列パラメーターにアクセスでき [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] <xref:System.AppDomain> ます。 詳細については、「 [方法: オンライン ClickOnce アプリケーションでクエリ文字列情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。

## <a name="example"></a>例
 次のコード例は、アプリケーションマニフェストの要素を示してい `entryPoint` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 このコード例は、 [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md) トピック用に用意されている、より大きな例の一部です。

```xml
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

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
