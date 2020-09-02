---
title: ソリューションの構成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solution configurations
ms.assetid: f22cfc75-3e31-4e0d-88a9-3ca99539203b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c96b73747ef8b136a74a7256cde7fef8d1c42de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705378"
---
# <a name="solution-configuration"></a>ソリューション構成
ソリューション構成には、ソリューションレベルのプロパティが格納します。 これらは、 **Start** (F5) キーと **Build** コマンドの動作を指示します。 既定では、これらのコマンドはデバッグ構成をビルドして開始します。 どちらのコマンドも、ソリューション構成のコンテキストで実行されます。 つまり、ユーザーは F5 キーを押して、アクティブなソリューションが設定を使用して構成されていることをすべてビルドすることができます。 この環境は、ビルドと実行の際にプロジェクトではなく、ソリューション用に最適化するように設計されています。

 標準の Visual Studio ツールバーには、[スタート] ボタンと、[スタート] ボタンの右側にある [ソリューション構成] ドロップダウンが表示されます。 この一覧では、ユーザーは、F5 キーを押したときに開始する構成を選択したり、独自のソリューション構成を作成したり、既存の構成を編集したりできます。

> [!NOTE]
> ソリューション構成を作成または編集するための機能拡張インターフェイスはありません。 `DTE.SolutionBuild` を使用する必要があります。 ただし、ソリューションビルドを管理するための機能拡張 Api もあります。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>」を参照してください。

 プロジェクトの種類でサポートされているソリューション構成を実装する方法を次に示します。

- Project

   現在のソリューションに存在するプロジェクトの名前を表示します。

- 構成

   プロジェクトの種類でサポートされている構成の一覧を提供し、プロパティページに表示するには、を実装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2> します。

   [構成] 列には、このソリューション構成でビルドするプロジェクト構成の名前が表示され、矢印ボタンをクリックすると、すべてのプロジェクト構成が一覧表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A>このリストに入力するには、環境でメソッドを呼び出します。 メソッドによって、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> プロジェクトが構成の編集をサポートしていることが示された場合、新しい選択または編集の選択は [構成] 見出しの下にも表示されます。 これらの各選択 `IVsCfgProvider2` は、プロジェクトの構成を編集するインターフェイスのメソッドを呼び出すダイアログボックスを起動します。

   プロジェクトで構成がサポートされていない場合、[構成] 列には [なし] が表示され、無効になります。

- プラットフォーム

   選択したプロジェクト構成のビルド対象のプラットフォームを表示し、矢印ボタンをクリックすると、そのプロジェクトで使用可能なすべてのプラットフォームが一覧表示されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A>このリストに入力するには、環境でメソッドを呼び出します。 メソッドによって、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A> プロジェクトがプラットフォームの編集をサポートしていることが示された場合は、[プラットフォーム] の見出しの下に新しい選択または編集の選択も表示されます。 これらの各選択は `IVsCfgProvider2` 、プロジェクトの使用可能なプラットフォームを編集するメソッドを呼び出すダイアログボックスを起動します。

   プロジェクトでプラットフォームがサポートされていない場合、そのプロジェクトの [プラットフォーム] 列には [なし] が表示され、は無効になります。

- Build

   現在のソリューション構成によってプロジェクトがビルドされるかどうかを指定します。 選択されていないプロジェクトは、プロジェクトの依存関係が含まれているにもかかわらず、ソリューションレベルのビルドコマンドが呼び出されてもビルドされません。 ビルド対象として選択されていないプロジェクトは、ソリューションのデバッグ、実行、パッケージ化、および配置にまだ含まれています。

- 配置

   選択したソリューションビルド構成で開始コマンドまたは配置コマンドが使用されたときに、プロジェクトを配置するかどうかを指定します。 このフィールドのチェックボックスは、プロジェクトがオブジェクトにインターフェイスを実装することによって配置をサポートしている場合に使用でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2> ます。

  新しいソリューション構成が追加されると、ユーザーは [標準] ツールバーの [ソリューション構成] ボックスの一覧からその構成を選択して、その構成をビルドまたは開始できます。

## <a name="see-also"></a>こちらもご覧ください
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
