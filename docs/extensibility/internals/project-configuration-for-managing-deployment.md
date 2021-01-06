---
title: 配置を管理するためのプロジェクト構成 |Microsoft Docs
description: デバッグとインストールに必要な場所への配置、および Visual Studio が配置をサポートするプロジェクトをサポートする2つの方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 5c322e320e193acd25a011cc85173c1c80e2d29d
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877989"
---
# <a name="project-configuration-for-managing-deployment"></a>展開の管理のためのプロジェクト構成
配置は、デバッグとインストールのために、ビルドプロセスから予想される場所に出力項目を物理的に移動する操作です。 たとえば、Web アプリケーションがローカルコンピューター上に構築され、サーバー上に配置される場合があります。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、配置にプロジェクトを参加させる2つの方法をサポートしています。

- デプロイプロセスの対象となります。

- デプロイプロセスのマネージャーとして。

  ソリューションを配置する前に、まず配置プロジェクトを追加して配置オプションを構成する必要があります。 Deploy プロジェクトがまだ存在しない場合は、[**ビルド**] メニューの [**ソリューションの配置**] をクリックするか、ソリューションを右クリックして、プロジェクトを作成するかどうかを確認するメッセージが表示されます。 **[はい]** をクリックすると、**リモート配置ウィザード** プロジェクトが選択された状態で [**新しいプロジェクトの追加**] ダイアログボックスが開きます。

  リモート配置ウィザードでは、アプリケーションの種類 (Windows または Web)、含めるプロジェクト出力グループ、含める追加ファイル、展開先のリモートコンピューターのいずれかを指定するよう求められます。 ウィザードの最後のページには、選択したオプションの概要が表示されます。

  配置プロセスの対象となるプロジェクトでは、代替環境に移動する必要がある出力項目が生成されます。 これらの出力項目は <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> 、プロジェクトが出力をグループ化できるようにする場合の主な目的として、インターフェイスのパラメーターとして記述されています。 の実装に関する詳細につい `IVsProjectCfg2` ては、「 [出力のプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)」を参照してください。

  配置プロセスを管理する配置プロジェクトでは、[配置] コマンドを有効にし、このコマンドを選択すると応答します。 配置プロジェクトは、配置を実行するインターフェイスを実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> し、配置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployStatusCallback> ステータスイベントを報告するためにインターフェイスを呼び出します。

  構成では、ビルドまたは配置操作に影響を与える依存関係を指定できます。 ビルドまたは配置の依存関係は、構成自体がビルドまたは配置される前または後にビルドまたは配置する必要があるプロジェクトです。 プロジェクト間のビルド依存関係についてはインターフェイスで説明 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency> し、インターフェイスを使用して依存関係を配置し <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency> ます。 詳細については、「 [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
