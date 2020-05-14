---
title: プロジェクトサブタイプ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 71dab4767c806b44cbd1f9638738b4a13d6b2bcb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706405"
---
# <a name="project-subtypes"></a>プロジェクト サブタイプ
プロジェクト サブタイプを使用すると、 のプロジェクト システムの動作[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をカスタマイズまたは調整できます。 カスタマイズには、プロジェクト ファイルに追加データを保存する、**新しい項目**の追加] ダイアログ ボックスで項目を追加またはフィルター処理する、アセンブリのデバッグと配置の方法の制御、プロジェクト**の [プロパティ ページ]** ダイアログ ボックスの拡張などがあります。 VSPackage は、COM 集約を使用してプロジェクトのサブタイプを実装します。

> [!NOTE]
> Visual C++ プロジェクト システムは、プロジェクトのサブタイプをサポートしていません。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]それ自体は、プロジェクト のサブタイプを使用して SQL Server およびスマート デバイス プロジェクトを実装します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクト サブタイプのデザイン](../../extensibility/internals/project-subtypes-design.md)

 プロジェクト サブタイプの概念について説明します。

- [プロジェクト サブタイプの初期化シーケンス](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

 プログラムによるプロジェクトのサブタイプ初期化シーケンスを環境別[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に記述します。

- [プロジェクト サブタイプによって拡張されるプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

 プロジェクト のサブタイプを使用して、最も頻繁に拡張される機能とメソッドの詳細な説明を示します。

- [MSBuild プロジェクト ファイルでのデータの保持](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

 プロジェクト ファイルにデータを保存する方法と、プロジェクト の<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>サブタイプ集計レベル全体でプロジェクト ファイル内のデータを保持する方法について説明します。

- [プロジェクト プロパティのユーザー インターフェイス](../../extensibility/internals/project-property-user-interface.md)

 プロジェクト のサブタイプでプロジェクトの **[プロパティ ページ]** ダイアログ ボックスを変更する方法について説明します。

- [ベース プロジェクトのオブジェクト モデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

 プロジェクト のサブタイプでオートメーション エクステンダーを使用してオートメーション オブジェクト モデルを拡張する方法について説明します。

- [[新しい項目の追加] ダイアログ ボックスへの投稿](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

 **[新しい**項目の追加] ダイアログ ボックスに項目を追加する方法について説明します。

- [プロジェクト ファイルでのデータの保存](../../extensibility/saving-data-in-project-files.md)

 プロジェクト のサブタイプが、パッケージ管理フレームワーク (MPF) を使用して、プロジェクト ファイル内のサブタイプ固有のデータを保存および取得する方法について説明します。

- [特別な展開の処理](../../extensibility/internals/handling-specialized-deployment.md)

 プロジェクト のサブタイプが、インターフェイスを実装することによって、特殊な<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>配置動作を提供する方法について説明します。

- [プロパティ ページの追加と削除](../../extensibility/adding-and-removing-property-pages.md)

 プロジェクト デザイナーでのプロパティ ページの追加と削除について説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 プロジェクトの詳細なトピックへの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]リンクを提供します。
