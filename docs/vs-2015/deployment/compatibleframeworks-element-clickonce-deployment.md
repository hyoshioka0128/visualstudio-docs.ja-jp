---
title: '&lt;互換フレームワーク &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <compatibleFrameworks> element [ClickOnce deployment manifest]
ms.assetid: f6c3ee55-9e65-403d-8664-3ebde872c7d4
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ef54062bd74c9395e187503dd12db1c0cd70d822
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675415"
---
# <a name="ltcompatibleframeworksgt-element-clickonce-deployment"></a>&lt;互換フレームワーク &gt; 要素 (ClickOnce 配置)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このアプリケーションをインストールして実行できる .NET Framework のバージョンを指定します。  
  
> [!NOTE]
> [MageUI.exe](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14) `compatibleFrameworks` [MageUI.exe](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)を使用して証明書で既に署名されているアプリケーションマニフェストを保存する場合、MageUI.exeは要素をサポートしません。 代わりに [Mage.exe](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1) を使用する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
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
 要素は、 `compatibleFrameworks` [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 以降で提供されるランタイムを対象とする配置マニフェストに必要です [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 。 `compatibleFrameworks`要素には `framework` 、このアプリケーションを実行できる .NET Framework バージョンを指定する1つ以上の要素が含まれています。 ランタイムは、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] この一覧で使用可能な最初のでアプリケーションを実行し `framework` ます。  
  
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
 次のコード例は、 `compatibleFrameworks` 配置マニフェストの要素を示して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] います。 このデプロイは、で実行でき [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] ます。 また、はのスーパーセットなので、でも実行でき [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] [!INCLUDE[net_client_v40_long](../includes/net-client-v40-long-md.md)] ます。  
  
```  
<compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">  
  <framework   
      targetVersion="4.0"   
      profile="Client"   
      supportedRuntime="4.0.30319" />  
</compatibleFrameworks>  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
