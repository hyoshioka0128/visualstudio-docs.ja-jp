---
title: ソリューション構成 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705378"
---
# <a name="solution-configuration"></a>ソリューション構成
ソリューション構成には、ソリューション レベルのプロパティが格納されます。 **スタート**(F5) キーと**ビルド**コマンドの動作を指示します。 既定では、これらのコマンドはデバッグ構成をビルドして開始します。 どちらのコマンドも、ソリューション構成のコンテキストで実行されます。 つまり、ユーザーは、設定を通じて構成されているアクティブなソリューションを F5 が起動してビルドすることを期待できます。 この環境は、ビルドと実行に関しては、プロジェクトではなくソリューションに最適化するように設計されています。

 標準の Visual Studio ツール バーには、[スタート] ボタンと [スタート] ボタンの右側にある [ソリューション構成] ドロップダウンが含まれています。 このリストでは、F5 を押したときに開始する構成を選択したり、独自のソリューション構成を作成したり、既存の構成を編集したりできます。

> [!NOTE]
> ソリューション構成を作成または編集するための機能拡張インターフェイスはありません。 `DTE.SolutionBuild` を使用する必要があります。 ただし、ソリューション ビルドを管理するための機能拡張 API があります。 詳細については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager2>」を参照してください。

 プロジェクトの種類でサポートされるソリューション構成を実装する方法を次に示します。

- Project

   現在のソリューションで見つかったプロジェクトの名前を表示します。

- 構成

   プロジェクトの種類でサポートされ、プロパティ ページに表示される構成の一覧を提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>するには、 を実装します。

   [構成] 列には、このソリューション構成でビルドするプロジェクト構成の名前が表示され、矢印ボタンをクリックすると、すべてのプロジェクト構成が一覧表示されます。 このリストに入力<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgNames%2A>するために、このメソッドが呼び出されます。 プロジェクトが<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>構成編集をサポートしていることを示している場合は、[新規] または [編集] の選択も [構成] 見出しの下に表示されます。 これらの選択のそれぞれは、プロジェクトの構成を編集するインターフェイス`IVsCfgProvider2`のメソッドを呼び出すダイアログ ボックスを起動します。

   プロジェクトが構成をサポートしていない場合は、[構成] 列に [なし] と表示され、無効になります。

- プラットフォーム

   選択したプロジェクト構成のビルド対象となるプラットフォームが表示され、矢印ボタンをクリックすると、プロジェクトで使用可能なすべてのプラットフォームが一覧表示されます。 このリストに入力<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetPlatformNames%2A>するために、このメソッドが呼び出されます。 プロジェクトが<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgProviderProperty%2A>プラットフォーム編集をサポートしていることを示している場合、新規または編集の選択もプラットフォームの見出しの下に表示されます。 これらの選択のそれぞれは、プロジェクトの利用可能な`IVsCfgProvider2`プラットフォームを編集するメソッドを呼び出すダイアログ ボックスを起動します。

   プロジェクトがプラットフォームをサポートしていない場合、そのプロジェクトのプラットフォーム列には[なし]と表示され、無効になります。

- ビルド

   プロジェクトが現在のソリューション構成によってビルドされるかどうかを指定します。 選択されていないプロジェクトは、ソリューション レベルのビルド コマンドが、プロジェクトの依存関係に関係なく呼び出されたときにビルドされません。 ビルド対象として選択されていないプロジェクトは、ソリューションのデバッグ、実行、パッケージ化、および配置に含まれます。

- 配置

   選択したソリューション ビルド構成で Start コマンドまたは Deploy コマンドを使用するときにプロジェクトを配置するかどうかを指定します。 このフィールドのチェック ボックスは、プロジェクトが<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg><xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>オブジェクトにインターフェイスを実装することによって配置をサポートしている場合に使用できます。

  新しいソリューション構成を追加すると、ユーザーは標準ツール バーの [ソリューション構成] ドロップダウン リスト ボックスからソリューション構成を選択して、その構成をビルドまたは開始できます。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
