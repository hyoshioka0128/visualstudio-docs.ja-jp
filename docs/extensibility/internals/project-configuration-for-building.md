---
title: ビルドのためのプロジェクト構成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], configuration for building
- project configurations, building
ms.assetid: 2c83615d-fa4d-4b9f-b315-7a69b3000da0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bdd084053e06206a99298b234b4d51c8504119a2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706727"
---
# <a name="project-configuration-for-building"></a>ビルドのためのプロジェクト構成
特定のソリューションのソリューション構成の一覧は、[ソリューション構成] ダイアログ ボックスで管理します。

 ユーザーは、独自の一意の名前を持つ追加のソリューション構成を作成できます。 ユーザーが新しいソリューション構成を作成すると、IDE はプロジェクト内の対応する構成名にデフォルト設定されます。 ユーザーは、必要に応じて特定の要件を満たすように選択を変更できます。 この動作の唯一の例外は、プロジェクトが新しいソリューション構成の名前と一致する構成をサポートする場合です。 たとえば、ソリューションに Project1 と Project2 が含まれているとします。 プロジェクト 1 には、デバッグ、リテール、および MyConfig1 のプロジェクト構成があります。 プロジェクト 2 には、デバッグ、リテール、および MyConfig2 のプロジェクト構成があります。

 ユーザーが MyConfig2 という名前の新しいソリューション構成を作成すると、Project1 は既定でデバッグ構成をソリューション構成にバインドします。 プロジェクト 2 は、既定で MyConfig2 構成をソリューション構成にバインドします。

> [!NOTE]
> バインディングは大文字と小文字を区別しません。

 ユーザーが構成ドロップダウン リストで **[複数選択]** 項目を選択すると、使用可能な構成の一覧を表示するダイアログ ボックスが表示されます。

 ![複数の構成](../../extensibility/internals/media/vsmultiplecfgs.gif "を持つ")複数の構成

 このダイアログ ボックスでは、ユーザーは 1 つまたは複数のコンフィギュレーションを選択できます。 選択すると、[プロパティ ページ] ダイアログ ボックスに表示されるプロパティ値に、選択したコンフィギュレーションの値の交差部分が反映されます。

 ソリューションおよびプロジェクトの[構成](../../extensibility/internals/solution-configuration.md)の追加と名前の変更に関する情報については、「ソリューション構成」を参照してください。

 プロジェクトの依存関係とビルド順序は、ソリューション構成に依存しません。 ソリューションまたはプロジェクトを右クリックし、[**プロジェクトの依存関係**] または [**プロジェクトのビルド順序**] オプションを選択すると、[**プロジェクトの依存関係**] ダイアログ ボックスが表示されます。 プロジェクト**メニューから**開く方法もあります。

 ![プロジェクトの依存関係](../../extensibility/internals/media/vsprojdependencies.gif "を行う")プロジェクトの依存関係

 プロジェクトの依存関係によって、プロジェクトのビルド順序が決まります。 ダイアログ ボックスの [ビルド順序] タブを使用して、ソリューション内のプロジェクトがビルドされる順序を正確に表示し、[依存関係] タブを使用してビルド順序を変更します。

> [!NOTE]
> リスト内のチェック ボックスがオンになっているが淡色表示になっているプロジェクトは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildDependency>または<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployDependency>インターフェイスによって明示的に指定された依存関係により、環境によって追加され、変更できません。 たとえば、プロジェクトから別のプロジェクトにプロジェクト[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]参照を追加すると、参照を削除することによってのみ削除できるビルド依存関係が自動的に追加されます。 チェック ボックスがオフで淡色表示されているプロジェクトは、依存関係ループが作成されるため (たとえば Project1 は Project2 に依存し、Project2 は Project1 に依存します)、ビルドが停止するため、選択できません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ビルド プロセスには、1 つの Build コマンドで呼び出される一般的なコンパイルおよびリンク操作が含まれます。 他にも、以前のビルドからすべての出力項目を削除するクリーン操作と、構成内の出力項目が変更されたかどうかを確認するための最新のチェックという 2 つのビルド プロセスもサポートできます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>オブジェクトは、ビルド<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>プロセスを管理<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>するために対応する ( から返される ) を返します。 ビルド操作の実行中にビルド操作の状態を報告するには、環境によって実装されたインターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildStatusCallback>とビルドステータスイベントに関心のあるその他のオブジェクトを、構成で呼び出します。

 構成設定をビルドすると、構成設定を使用して、デバッガーの制御下で実行できるかどうかを判断できます。 デバッグを<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>サポートするために構成が実装されます。

 プロジェクトの依存関係を実装した後、オートメーション モデルを使用して依存関係をプログラムで操作できます。 オートメーション<xref:EnvDTE.SolutionBuild.BuildDependencies%2A>モデルを呼び出します。 ソリューション ビルド マネージャーの構成とそのプロパティを直接操作できる、使用可能な VSIP API レベルのインターフェイスはありません。

 また、プロジェクトの依存関係ウィンドウにグリッドを指定することもできます。 詳細については、「[プロパティの表示グリッド](../../extensibility/internals/properties-display-grid.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [展開の管理のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-managing-deployment.md)
- [出力のためのプロジェクト構成](../../extensibility/internals/project-configuration-for-output.md)
