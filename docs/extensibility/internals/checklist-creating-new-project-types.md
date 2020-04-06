---
title: 'チェックリスト : 新しいプロジェクトタイプの作成 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5963083239571af43012e1a79576ee80846d80bd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709747"
---
# <a name="checklist-create-new-project-types"></a>チェックリスト: 新しいプロジェクトの種類を作成する
新しいプロジェクトの種類を作成するには、いくつかのタスクを完了する必要があります。 次のチェックリストは、これらのタスクのガイドを提供します。

1. 新しいプロジェクトの種類の機能をデザインします。 詳細については、「[プロジェクトの種類の設計に関する決定](../../extensibility/internals/project-type-design-decisions.md)事項」を参照してください。

2. コードやその他のプロジェクト要素に使用するエディターを決定します。 コア エディタまたは標準エディタを使用することも、プロジェクト固有のエディタを作成して使用することもできます。 詳細については、「カスタム[エディターとデザイナーを作成する](../../extensibility/creating-custom-editors-and-designers.md)」および「[方法 : プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」を参照してください。

3. プロジェクト項目が**クラス ビュー**およびオブジェクト ブラウザに参加するレベルを決定**します**。 詳細については、「[シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)」を参照してください。

4. プロジェクトおよびプロジェクト項目に対して以前に行った設計上の決定に基づいて、新しいクラスを派生させます。

5. 次のプロジェクトタイプコンポーネントのコードを記述します。

    - プロジェクト ファクトリ:新しいプロジェクトの作成と既存のプロジェクトのオープンを管理します。 詳細については、「[プロジェクト ファクトリを使用してプロジェクト インスタンスを作成する](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。

    - プロジェクト階層とコマンド処理。 詳細については、「 [HierUtil7 プロジェクト クラスを使用してプロジェクトの種類を実装する (C++)、](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)[プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)、[プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)、および[MenuCommands と OleMenuCommands](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)」を参照してください。

    - プロジェクト項目の管理 (プロジェクトを **[新しいプロジェクト**] ダイアログ ボックスに追加するなど)。 詳細については、「[プロジェクトテンプレートとプロジェクト項目テンプレートの追加」および「プロジェクトテンプレートと項目テンプレート](../../extensibility/internals/adding-project-and-project-item-templates.md)[の登録](../../extensibility/internals/registering-project-and-item-templates.md)」を参照してください。

    - プロジェクトの状態と個々の項目の永続性。 詳細については、「[プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する 」を参照してください。 ソリューション情報の永続化については、「[ソリューション](../../extensibility/internals/solutions-overview.md)」を参照してください。

    - [プロパティ] ウィンドウに表示する構成に依存しないプロパティ。 詳細については、「[プロパティの拡張](../../extensibility/internals/extending-properties.md)」を参照してください。

    - 構成に依存するプロパティを表示するプロパティ ページに実装されているプロジェクト構成プロパティ。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

    - 展開用の出力を列挙します。 詳細については、「[出力用のプロジェクト構成」を](../../extensibility/internals/project-configuration-for-output.md)参照してください。

    - プロジェクトスタートアップ サービス。 詳細については、「プロジェクト[モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)」および[「プロジェクト モデルのコア コンポーネント](../../extensibility/internals/project-model-core-components.md)」を参照してください。

    - オートメーションで使用できるオブジェクト、`IDispatch`または から派生したクラス。

    - XML コマンド テーブル (*.vsct*) ファイル。 詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

6. プロジェクトの種類をテスト、デバッグ、および開始します。

7. [**参照の追加**] ダイアログ ボックスの [**プロジェクト**]`VARIANT_TRUE`タブでプロジェクトを`VSHPROPID_ShowProjInSolutionPage`表示するには、 の値を設定します。 詳細については、「 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>」を参照してください。

8. VS パッケージをインストールするための Microsoft インストーラ (*.msi*) ファイルを作成します。 詳細については、「 [VSPackage を Windows インストーラでインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)[する](../../extensibility/internals/registering-a-project-type.md)」を参照[してください。](../../extensibility/internals/vspackages.md)

## <a name="see-also"></a>関連項目
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [プロジェクトタイプを作成する場合](../../extensibility/internals/when-to-create-project-types.md)
- [プロジェクト タイプの作成](../../extensibility/internals/creating-project-types.md)
