---
title: ClickOnce キャッシュの概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 58ea758ea10e2c58ff123a2bc991f14191db0aa1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151666"
---
# <a name="clickonce-cache-overview"></a>ClickOnce キャッシュの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ローカルにインストールされているか、オンラインでホストされているすべての [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションは、クライアントコンピューターのアプリケーションキャッシュに格納され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 *cache* [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]キャッシュは、現在のユーザーの [ドキュメントと設定] フォルダーの [ローカル設定] ディレクトリにある非表示ディレクトリのファミリです。 このキャッシュは、アセンブリ、構成ファイル、アプリケーションとユーザー設定、およびデータディレクトリを含む、アプリケーションのすべてのファイルを保持します。 キャッシュは、アプリケーションのデータディレクトリを最新バージョンに移行する役割も担います。 データ移行の詳細については、「 [ClickOnce アプリケーションにおけるローカルデータおよびリモートデータへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)」を参照してください。  
  
 アプリケーションストレージ用に1つの場所を提供することにより、は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ユーザーからアプリケーションの物理的なインストールを管理するタスクを引き継ぎます。 また、キャッシュは、すべてのアプリケーションのアセンブリとデータファイルと、個別のバージョンを相互に分離して、アプリケーションを分離するのにも役立ちます。 たとえば、アプリケーションをアップグレードすると、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] そのバージョンとそのデータリソースはキャッシュ内に独自のディレクトリと共に提供されます。  
  
## <a name="cache-storage-quota"></a>キャッシュストレージクォータ  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] オンラインでホストされているアプリケーションは、キャッシュのサイズを制限するクォータによって占有される領域の量に制限され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 キャッシュサイズは、すべてのユーザーのオンラインアプリケーションに適用されます。部分的に信頼された1つのオンラインアプリケーションは、クォータ領域の半分に制限されます。 インストールされているアプリケーションはキャッシュサイズによって制限されず、キャッシュの制限にはカウントされません。 すべてのアプリケーションについて、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] キャッシュには現在のバージョンと以前にインストールされたバージョンのみが保持されます。  
  
 既定では、クライアントコンピューターには、オンラインアプリケーション用に 250 MB の記憶域があり [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 データファイルは、この制限にはカウントされません。 システム管理者は、レジストリ HKEY_CURRENT_USER キー \Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB を変更することにより、特定のクライアントコンピューターのこのクォータを拡大または縮小できます。これは、キャッシュサイズを kb 単位で表す DWORD 値です。 たとえば、キャッシュサイズを 50 MB に減らすために、この値を51200に変更します。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
