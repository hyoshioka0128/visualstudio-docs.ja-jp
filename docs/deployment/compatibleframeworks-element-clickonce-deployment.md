---
title: '&lt;互換フレームワーク &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99db3d51414197df469aaa2eabe97e0967c31b05
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "66746041"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;互換フレームワーク &gt; 要素 (ClickOnce 配置)
このアプリケーションをインストールして実行できる .NET Framework のバージョンを指定します。

> [!NOTE]
> [*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client) `compatibleFrameworks` [*MageUI.exe*](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)を使用して証明書で既に署名されているアプリケーションマニフェストを保存する場合、MageUI.exeは要素をサポートしません。 代わりに、 [*Mage.exe*](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)を使用する必要があります。

## <a name="syntax"></a>構文

```xml
<compatibleFrameworks
      SupportUrl> 
   <framework
      targetVersion
      profile
      supportedRuntime
   /> 
</ compatibleFrameworks>
```

## <a name="elements-and-attributes"></a>要素と属性
 `compatibleFrameworks`要素は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] .NET Framework 4 以降で提供されるランタイムを対象とする配置マニフェストに必要です。 `compatibleFrameworks`要素には `framework` 、このアプリケーションを実行できる .NET Framework バージョンを指定する1つ以上の要素が含まれています。 ランタイムは、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] この一覧で使用可能な最初のでアプリケーションを実行し `framework` ます。

 次の表に、要素がサポートする属性を示し `compatibleFrameworks` ます。

|属性|説明|
|---------------|-----------------|
|`S` `upportUrl`|省略可能。 互換性のある適切な .NET Framework バージョンをダウンロードできる URL を指定します。|

## <a name="framework"></a>フレームワーク
 必須。 次の表に、要素がサポートする属性を示し `framework` ます。

|属性|説明|
|---------------|-----------------|
|`targetVersion`|必須。 ターゲット .NET Framework のバージョン番号を指定します。|
|`profile`|必須。 ターゲット .NET Framework のプロファイルを指定します。|
|`supportedRuntime`|必須。 ターゲット .NET Framework に関連付けられているランタイムのバージョン番号を指定します。|

## <a name="remarks"></a>解説

## <a name="example"></a>例
 次のコード例は、 `compatibleFrameworks` 配置マニフェストの要素を示して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] います。 このデプロイは、で実行でき [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] ます。 また、.NET Framework 4 でも実行できます。これは、のスーパーセットであるため [!INCLUDE[net_client_v40_long](../deployment/includes/net_client_v40_long_md.md)] です。

```xml
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">
  <framework
      targetVersion="4.0"
      profile="Client"
      supportedRuntime="4.0.30319" />
</compatibleFrameworks>
```

## <a name="see-also"></a>関連項目
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)