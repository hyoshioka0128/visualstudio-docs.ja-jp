---
title: '&lt;deployment &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
description: Deployment 要素は、更新の展開およびシステムへの公開に使用される属性を識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#subscription
- urn:schemas-microsoft-com:asm.v2#beforeApplicationStartup
- urn:schemas-microsoft-com:asm.v2#deploymentProvider
- urn:schemas-microsoft-com:asm.v2#update
- urn:schemas-microsoft-com:asm.v2#deployment
- urn:schemas-microsoft-com:asm.v2#expiration
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <deployment> element [ClickOnce deployment manifest]
ms.assetid: 4fafa9c2-97a0-4cea-b8fd-9746dca33af4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3252c8f305b97564b8fb19affa83cc7dd837c97d
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382859"
---
# <a name="ltdeploymentgt-element-clickonce-deployment"></a>&lt;deployment &gt; 要素 (ClickOnce 配置)
更新プログラムの配置とシステムへの公開に使用される属性を指定します。

## <a name="syntax"></a>構文

```xml

      <deployment
   install
   minimumRequiredVersion
   mapFileExtensions
   disallowUrlActivation
   trustUrlParameters
>
   <subscription>
         <update>
            <beforeApplicationStartup/>
            <expiration
               maximumAge
               unit
            />
         </update>
   </subscription>
   <deploymentProvider
      codebase
   />
</deployment>
```

## <a name="elements-and-attributes"></a>要素と属性
 `deployment` 要素は必須です。この要素は `urn:schemas-microsoft-com:asm.v2` 名前空間にあります。 要素には、次の属性があります。

| 属性 | 説明 |
|--------------------------| - |
| `install` | 必須。 このアプリケーションが Windows の [ **スタート** ] メニューと [コントロールパネル] の [ **プログラムの追加と削除** ] アプリケーションでプレゼンスを定義するかどうかを指定します。 有効な値は `true` と `false` です。 `false`の場合、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は常に、このアプリケーションの最新バージョンをネットワークから実行し、要素を認識しません `subscription` 。 |
| `minimumRequiredVersion` | 省略可能。 クライアントで実行できる、このアプリケーションの最小バージョンを指定します。 アプリケーションのバージョン番号が配置マニフェストで指定されたバージョン番号よりも小さい場合、アプリケーションは実行されません。 バージョン番号は、という形式で指定する必要があり `N.N.N.N` ます。ここで、 `N` は符号なし整数です。 属性がの場合、を設定することはでき `install` `false` `minimumRequiredVersion` ません。 |
| `mapFileExtensions` | 省略可能。 既定値は `false` です。 の場合 `true` 、配置内のすべてのファイルに .deploy 拡張子が必要です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、これらのファイルを Web サーバーからダウンロードするとすぐに、この拡張機能を削除します。 を使用してアプリケーションを発行すると [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、この拡張機能がすべてのファイルに自動的に追加されます。 このパラメーターを使用すると、配置内のすべてのファイル [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を Web サーバーからダウンロードして、.exe などの "安全でない" 拡張機能で終わるファイルの転送をブロックすることができます。 |
| `disallowUrlActivation` | 省略可能。 既定値は `false` です。 `true`の場合、インストールされているアプリケーションは、url をクリックするか、Internet Explorer に url を入力することで起動できなくなります。 `install`属性が存在しない場合、この属性は無視されます。 |
| `trustURLParameters` | 省略可能。 既定値は `false` です。 の場合、 `true` アプリケーションに渡されるクエリ文字列パラメーターを URL に含めることができます。コマンドライン引数はコマンドラインアプリケーションに渡されます。 詳細については、「 [方法: オンライン ClickOnce アプリケーションでクエリ文字列情報を取得する](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)」を参照してください。<br /><br /> 属性がの場合は `disallowUrlActivation` `true` 、 `trustUrlParameters` マニフェストから除外するか、を明示的にに設定する必要があり `false` ます。 |

 要素には `deployment` 、次の子要素も含まれます。

## <a name="subscription"></a>subscription
 省略可能。 要素が含まれてい `update` ます。 `subscription` 要素に属性はありません。 要素が存在しない場合 `subscription` 、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは更新プログラムをスキャンしません。 `install`要素の属性がの場合 `deployment` `false` 、要素は `subscription` 無視されます。これは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ネットワークから起動されるアプリケーションが常に最新バージョンを使用するためです。

## <a name="update"></a>update
 必須。 この要素は要素の子で `subscription` あり、要素または要素で構成され `beforeApplicationStartup` `expiration` ます。 `beforeApplicationStartup` との `expiration` 両方を同じ配置マニフェストで指定することはできません。

 `update` 要素に属性はありません。

## <a name="beforeapplicationstartup"></a>beforeApplicationStartup
 省略可能。 この要素は要素の子であり、 `update` 属性はありません。 要素が `beforeApplicationStartup` 存在する場合、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] クライアントがオンラインになっている場合は、が更新プログラムを確認するときに、アプリケーションがブロックされます。 この要素が存在しない場合、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、最初に要素に指定された値に基づいて更新プログラムをスキャンし `expiration` ます。 `beforeApplicationStartup` との `expiration` 両方を同じ配置マニフェストで指定することはできません。

## <a name="expiration"></a>expiration
 省略可能。 この要素は要素の子で `update` あり、子はありません。 `beforeApplicationStartup` との `expiration` 両方を同じ配置マニフェストで指定することはできません。 更新プログラムのチェックが行われ、更新されたバージョンが検出されると、既存のバージョンが実行されている間に新しいバージョンがキャッシュされます。 その後、アプリケーションの次回の起動時に、新しいバージョンがインストールされ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

 要素は、 `expiration` 次の属性をサポートしています。

|属性|説明|
|---------------|-----------------|
|`maximumAge`|必須。 アプリケーションが更新プログラムのチェックを実行する前に、現在の更新プログラムがどのようになるかを指定します。 時間の単位は、属性によって決まり `unit` ます。|
|`unit`|必須。 の時間単位を識別 `maximumAge` します。 有効な単位は `hours` 、、 `days` 、および `weeks` です。|

## <a name="deploymentprovider"></a>deploymentProvider
 .NET Framework 2.0 の場合、配置マニフェストにセクションが含まれている場合、この要素は必須です `subscription` 。 .NET Framework 3.5 以降では、この要素は省略可能であり、配置マニフェストが検出されたサーバーとファイルパスに既定で設定されます。

 この要素は `deployment` 要素の子であり、以下の属性があります。

| 属性 | 説明 |
|------------| - |
| `codebase` | 必須。 アプリケーションの更新に使用される配置マニフェストの場所を Uniform Resource Identifier (URI) で識別し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 また、この要素により、CD ベースのインストールの更新プログラムの場所も転送できます。 有効な URI である必要があります。 |

## <a name="remarks"></a>Remarks
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]スタートアップ時に更新プログラムをスキャンしたり、起動後に更新プログラムをスキャンしたり、更新プログラムを確認したりしないようにアプリケーションを構成できます。 スタートアップ時に更新プログラムをスキャンするには、要素が要素の下に存在することを確認し `beforeApplicationStartup` `update` ます。 スタートアップ後に更新プログラムをスキャンするには、要素の `expiration` 下に要素が存在 `update` し、その更新間隔が指定されていることを確認します。

 更新プログラムの確認を無効にするには、要素を削除し `subscription` ます。 配置マニフェストで更新プログラムをスキャンしないように指定した場合でも、メソッドを使用して更新プログラムを手動で確認でき <xref:System.Deployment.Application.ApplicationDeployment.CheckForUpdate%2A> ます。

 DeploymentProvider が更新プログラムにどのように関連しているかの詳細については、「 [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)」を参照してください。

## <a name="examples"></a>例
 次のコード例は、 `deployment` 配置マニフェストの要素を示してい [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 この例では、要素を使用し `deploymentProvider` て、優先する更新の場所を示しています。

```xml
<deployment install="true" minimumRequiredVersion="2.0.0.0" mapFileExtension="true" trustUrlParameters="true">
    <subscription>
      <update>
        <expiration maximumAge="6" unit="hours" />
      </update>
    </subscription>
    <deploymentProvider codebase="http://www.adatum.com/MyApplication.application" />
  </deployment>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)