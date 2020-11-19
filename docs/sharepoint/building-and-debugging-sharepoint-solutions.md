---
title: SharePoint ソリューションのビルドとデバッグ | Microsoft Docs
description: SharePoint ソリューションのビルドとデバッグについて説明し、Visual Studio で他の種類のプロジェクトをビルドおよびデバッグする場合との違いについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, building and debugging
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f6801f6b60d2ef522385ecdf290d0a1913bd6df2
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850222"
---
# <a name="build-and-debug-sharepoint-solutions"></a>SharePoint ソリューションのビルドとデバッグ
  一般に、SharePoint ソリューションをビルドおよびデバッグするのは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でその他の種類のプロジェクトをビルドおよびデバッグするのと同じです。 このセクションのトピックでは、いくつかある相違点について説明します。

## <a name="project-output-for-sharepoint-solutions"></a>SharePoint ソリューションのプロジェクト出力
 SharePoint ソリューションをビルドすると、アセンブリおよびソリューション パッケージ ( *.wsp*) ファイルが作成されます。 次の表に、ビルド時にこれらのファイルが置かれる場所を示します。

|ビルド項目|出力先フォルダー|
|----------------|-------------------|
|アセンブリ、プログラム データベース ( *.pdb*)、および *.wsp* ファイル。|*\<ProjectName>\bin\debug* または *\<ProjectName>\bin\release*|
|SharePoint プロジェクト項目ファイル。|*\<ProjectName>\pkg\debug* または *\<ProjectName>\pkg\release*|
|ビルド中間ファイル。|*\<ProjectName>\obj\debug* または *\<ProjectName>\obj\release*|
|パッケージ中間ファイル。|*\<ProjectName>\pkgobj\debug* または *\<ProjectName>\pkgobj\release*|

## <a name="build-sharepoint-solutions"></a>SharePoint ソリューションをビルドする
 SharePoint ソリューションをビルドするには、開発用コンピューターに適切なバージョンの SharePoint サーバーがインストールされている必要があります。 それ以外は、SharePoint ソリューションをビルドする方法は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で他の種類のプロジェクトをビルドする方法と同じです。 詳細については、「[方法:SharePoint ソリューションをビルドする](../sharepoint/how-to-build-sharepoint-solutions.md)」を参照してください。

## <a name="debug-and-test-sharepoint-solutions"></a>SharePoint ソリューションをデバッグしてテストする
 デバッグの前に、[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] では *.wsp* パッケージが SharePoint サーバーにコピーされ、サイトおよび Web スコープの機能がアクティブにされ、場合によっては、プロジェクトが開始されます。 他のケースでは、プロジェクトを手動で開くことが必要な場合があります。 詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」および「[SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」を参照してください。

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>Azure DevOps Services 機能を使用して SharePoint ソリューションをデバッグおよび検証する
 単体テストや IntelliTrace などの Azure DevOps Services 機能を使用すると、SharePoint ソリューションの問題をより正確に特定することができます。 プロファイルを使用すると、SharePoint ソリューション内でパフォーマンスの問題が生じている領域を特定し、識別することができます。 詳細については、「[SharePoint コードの検証とデバッグ](../sharepoint/verifying-and-debugging-sharepoint-code.md)」および「[SharePoint アプリケーションのパフォーマンスのプロファイリング](../sharepoint/profiling-the-performance-of-sharepoint-applications.md)」を参照してください。

## <a name="security-during-the-build-process"></a>ビルド処理中のセキュリティ
 SharePoint ソリューションをパッケージ化または配置するには、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] に、SharePoint サーバーにファイルをコピーするためのアクセス許可が必要です。 管理者特権プロセスとして [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を実行する必要があります。ご利用のユーザー アカウントは SharePoint サーバー上のサイト コレクション管理者とする必要があります。 さらに、プロジェクトがサンドボックス ソリューションとファーム ソリューションのどちらであるかを指定する必要があります。 詳細については、「[サンドボックス ソリューションとファーム ソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)」を参照してください。

## <a name="using-the-clean-command"></a>[クリーン] コマンドの使用
 SharePoint ソリューションがデバッグのために SharePoint サーバーにインストールされている場合、 **[クリーン]** コマンドを実行しても、ソリューションはアンインストールされません。 代わりに、SharePoint の構成を介して [機能] を非アクティブ化する必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
