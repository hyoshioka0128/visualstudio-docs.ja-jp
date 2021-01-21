---
title: サンドボックスソリューションとファームソリューションの違い |Microsoft Docs
description: サンドボックスソリューションとファームソリューションの違いについて説明します。 どちらの種類のソリューションでも Visual Studio がデバッグにどのように近づいているかを理解します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 25c1c9047ba9e38e3e652abcbe92ce6575d7b750
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672783"
---
# <a name="differences-between-sandboxed-and-farm-solutions"></a>サンドボックスソリューションとファームソリューションの違い
  SharePoint ソリューションをコンパイルすると、sharepoint サーバーに配置され、デバッガーがアタッチされてデバッグされます。 ソリューションのデバッグに使用されるプロセスは、サンドボックスソリューションのプロパティの設定 (サンドボックスソリューションまたはファームソリューション) によって異なります。

 詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

## <a name="farm-solutions"></a>ファームソリューション
 IIS ワーカープロセス (W3WP.exe) でホストされているファームソリューションは、ファーム全体に影響を与える可能性のあるコードを実行します。 "サンドボックスソリューション" プロパティが "ファームソリューション" に設定されている SharePoint プロジェクトをデバッグする場合、IIS ワーカープロセスによってロックされているすべてのファイルを解放するために、SharePoint が機能を取り消すか配置する前に、システムの IIS アプリケーションプールがリサイクルされます。 SharePoint プロジェクトのサイトの URL を提供している IIS アプリケーションプールのみがリサイクルされます。

## <a name="sandboxed-solutions"></a>サンドボックスソリューション
 SharePoint ユーザーコードソリューションワーカープロセス (SPUCWorkerProcess.exe) でホストされるサンドボックスソリューションは、ソリューションのサイトコレクションにのみ影響を与えるコードを実行します。 サンドボックスソリューションは IIS ワーカープロセスでは実行されないため、IIS アプリケーションプールも IIS サーバーも再起動する必要はありません。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Spucworkerprocess.exe プロセスにデバッガーをアタッチします。これは、SharePoint の SPUserCodeV4 サービスが自動的にトリガーおよび制御します。 Spucworkerprocess.exe プロセスをリサイクルして最新バージョンのソリューションを読み込む必要はありません。

## <a name="either-type-of-solution"></a>どちらの種類のソリューションでも
 どちらのソリューションタイプで [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] も、はデバッガーをブラウザーにアタッチして、クライアント側のスクリプトのデバッグを有効にします。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、この目的にスクリプトデバッグエンジンを使用します。 スクリプトのデバッグを有効にするには、プロンプトが表示されたら、既定のブラウザーの設定を変更する必要があります。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 現在のサイトを実行している w3wp.exe または Spucworkerprocess.exe プロセスにのみデバッガーをアタッチします。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] マネージ COM + とワークフローデバッグエンジンもアタッチします。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [サンドボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)
