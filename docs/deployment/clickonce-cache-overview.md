---
title: ClickOnce キャッシュの概要 |Microsoft Docs
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3d7abeeec4a640119e3089c795ac529a10f8dc09
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84182626"
---
# <a name="clickonce-cache-overview"></a>ClickOnce キャッシュの概要
ローカルにインストールされているか、オンラインでホストされているすべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、クライアントコンピューターのアプリケーションキャッシュに格納され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 *cache* [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]キャッシュは、現在のユーザーの [ドキュメントと設定] フォルダーの [ローカル設定] ディレクトリにある非表示ディレクトリのファミリです。 このキャッシュは、アセンブリ、構成ファイル、アプリケーションとユーザー設定、およびデータディレクトリを含む、アプリケーションのすべてのファイルを保持します。 キャッシュは、アプリケーションのデータディレクトリを最新バージョンに移行する役割も担います。 データ移行の詳細については、「 [ClickOnce アプリケーションにおけるローカルデータおよびリモートデータへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)」を参照してください。

 アプリケーションストレージ用に1つの場所を提供することにより、は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ユーザーからアプリケーションの物理的なインストールを管理するタスクを引き継ぎます。 また、キャッシュは、すべてのアプリケーションのアセンブリとデータファイルと、個別のバージョンを相互に分離して、アプリケーションを分離するのにも役立ちます。 たとえば、アプリケーションをアップグレードすると、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] そのバージョンとそのデータリソースはキャッシュ内に独自のディレクトリと共に提供されます。

## <a name="cache-storage-quota"></a>キャッシュストレージクォータ
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]オンラインでホストされているアプリケーションは、キャッシュのサイズを制限するクォータによって占有される領域の量に制限され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 キャッシュサイズは、すべてのユーザーのオンラインアプリケーションに適用されます。部分的に信頼された1つのオンラインアプリケーションは、クォータ領域の半分に制限されます。 インストールされているアプリケーションはキャッシュサイズによって制限されず、キャッシュの制限にはカウントされません。 すべてのアプリケーションについて、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] キャッシュには現在のバージョンと以前にインストールされたバージョンのみが保持されます。

 既定では、クライアントコンピューターには、オンラインアプリケーション用に 250 MB の記憶域があり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 データファイルは、この制限にはカウントされません。 システム管理者は、レジストリ**HKEY_CURRENT_USER キー \software\classes\software\microsoft\windows\currentversion\deployment\onlineappquotainkb**を変更することにより、特定のクライアントコンピューターのこのクォータを拡大または縮小できます。これは、キャッシュサイズを kb 単位で表す DWORD 値です。 たとえば、キャッシュサイズを 50 MB に減らすために、この値を51200に変更します。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)