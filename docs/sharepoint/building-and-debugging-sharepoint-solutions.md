---
title: SharePoint ソリューションのビルドとデバッグ |Microsoft Docs
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
ms.openlocfilehash: e4b34df23c8cb612d72fed108a6c0aecbf57875c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016362"
---
# <a name="build-and-debug-sharepoint-solutions"></a>SharePoint ソリューションのビルドとデバッグ
  一般に、SharePoint ソリューションのビルドとデバッグは、で他の種類のプロジェクトをビルドおよびデバッグすることと同じです [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 このセクションのトピックでは、いくつかある相違点について説明します。

## <a name="project-output-for-sharepoint-solutions"></a>SharePoint ソリューションのプロジェクト出力
 SharePoint ソリューションを構築すると、アセンブリとソリューションパッケージ (*.wsp*) ファイルが作成されます。 次の表は、ビルド時のこれらのファイルの場所を示しています。

|ビルド項目|出力先フォルダー|
|----------------|-------------------|
|アセンブリ、プログラムデータベース (*.pdb*)、および *.wsp*ファイル。|* \<ProjectName> \bin\debug*または* \<ProjectName> \bin\release*|
|SharePoint プロジェクトアイテムファイル。|* \<ProjectName> \pkg\debug*または* \<ProjectName> \ pkg\ リリース*|
|中間ファイルをビルドします。|* \<ProjectName> \obj\debug*または* \<ProjectName> \ obj\ リリース*|
|中間ファイルをパッケージ化します。|* \<ProjectName> \pkgobj\debug*または* \<ProjectName> \ pkgobj\ リリース*|

## <a name="build-sharepoint-solutions"></a>SharePoint ソリューションのビルド
 SharePoint ソリューションをビルドするには、開発用コンピューターに適切なバージョンの SharePoint server がインストールされている必要があります。 そうしないと、SharePoint ソリューションの構築は、で他の種類のプロジェクトをビルドする場合と同じに [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] なります。 詳細については、「[方法: SharePoint ソリューションをビルド](../sharepoint/how-to-build-sharepoint-solutions.md)する」を参照してください。

## <a name="debug-and-test-sharepoint-solutions"></a>SharePoint ソリューションのデバッグとテスト
 デバッグする前に、では、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] *.wsp*パッケージが SharePoint サーバーにコピーされ、サイトと Web スコープの機能がアクティブ化されます。また、場合によっては、によってプロジェクトが開始されます。 場合によっては、プロジェクトを手動で開く必要があります。 詳細については、「 [sharepoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」および「 [Sharepoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」を参照してください。

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>Azure DevOps Services 機能を使用して SharePoint ソリューションをデバッグおよび検証する
 単体テストや IntelliTrace などの Azure DevOps Services 機能を使用すると、SharePoint ソリューションの問題をより正確に特定できます。 プロファイルを使用すると、SharePoint ソリューションのパフォーマンス問題の領域を特定し、特定することができます。 詳細については、「sharepoint[コードの検証およびデバッグ](../sharepoint/verifying-and-debugging-sharepoint-code.md)」および「 [Sharepoint アプリケーションのパフォーマンスのプロファイリング](../sharepoint/profiling-the-performance-of-sharepoint-applications.md)」を参照してください。

## <a name="security-during-the-build-process"></a>ビルド処理中のセキュリティ
 SharePoint ソリューションをパッケージ化または配置するには、が [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sharepoint サーバーにファイルをコピーするためのアクセス許可を持っている必要があります。 を [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 昇格されたプロセスとして実行する必要があります。また、ユーザーアカウントは SharePoint サーバーのサイトコレクション管理者である必要があります。 さらに、プロジェクトがサンドボックスソリューションとファームソリューションのどちらであるかを指定する必要があります。 詳細については、「[サンドボックスソリューションとファームソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)」を参照してください。

## <a name="using-the-clean-command"></a>Clean コマンドの使用
 Sharepoint ソリューションがデバッグのために SharePoint サーバーにインストールされている場合、[**クリーン**] コマンドを実行してもソリューションはアンインストールされません。 代わりに、SharePoint の構成を使用して機能を非アクティブ化する必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [サーバーエクスプローラーを使用した SharePoint 接続の参照](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
