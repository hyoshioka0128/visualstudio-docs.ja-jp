---
title: 配置を管理するためのプロジェクト構成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, managing deployment
- projects [Visual Studio SDK], configuration for managing deployment
ms.assetid: bd5940d9-d94d-4944-beda-4ec1ab2bbde5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 62f7bf6535a89e46799ade88fe8976974b3019c5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706712"
---
# <a name="project-configuration-for-managing-deployment"></a>展開の管理のためのプロジェクト構成
配置とは、ビルド 処理からデバッグおよびインストールの必要な場所に出力項目を物理的に移動する処理です。 たとえば、Web アプリケーションをローカル コンピュータ上に構築し、サーバーに配置します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトを配置に関与させる 2 つの方法をサポートします。

- 展開プロセスの対象として。

- 展開プロセスのマネージャーとして。

  ソリューションを配置する前に、配置プロジェクトを追加して配置オプションを構成する必要があります。 配置プロジェクトが存在しない場合は、[**ビルド**] メニューの [**ソリューションの配置**] を選択するか、ソリューションを右クリックして作成するかの確認を求められます。 [**はい**] をクリックすると、[**新しいプロジェクトの追加**] ダイアログ ボックスが開き、**リモート配置ウィザード**プロジェクトが選択されます。

  リモート配置ウィザードでは、アプリケーションの種類 (Windows または Web)、含めるプロジェクト出力グループ、追加ファイル、および配置先のリモート コンピュータを指定します。 ウィザードの最後のページには、選択したオプションの概要が表示されます。

  配置プロセスの対象となるプロジェクトは、別の環境に移動する必要がある出力項目を生成します。 これらの出力項目は、プロジェクトが出力を<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>グループ化できるようにする場合の主な目的を持つインターフェースのパラメーターとして記述されます。 の`IVsProjectCfg2`実装に関連する詳細については、「[出力プロジェクトの構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

  配置プロセスを管理する配置プロジェクトは、[配置] コマンドを有効にし、このコマンドが選択されたときに応答します。 配置プロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>配置を実行し、配置状態イベントを報告<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback>するインターフェイスを呼び出すインターフェイスを実装します。

  構成では、ビルドまたは配置操作に影響する依存関係を指定できます。 ビルドまたは配置の依存関係とは、構成自体がビルドまたは配置される前または後にビルドまたは配置する必要があるプロジェクトです。 プロジェクト間のビルド依存関係は<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency>、インターフェイスで説明され、インターフェイスと依存関係を<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>配置します。 詳細については、「[ビルド用のプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
