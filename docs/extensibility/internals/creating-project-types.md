---
title: プロジェクトタイプの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d2398b63b8cd52784252cfc764bb6c6a30e1accc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709078"
---
# <a name="create-project-types"></a>プロジェクト タイプの作成
新しいプロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]タイプを作成することで拡張できます。 新しいプロジェクトタイプを作成するには、いくつかの概念を理解し、いくつかのステップを完了する必要があります。 次のトピックでは、プロジェクトの種類を作成する方法の概要を説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトタイプ設計の決定](../../extensibility/internals/project-type-design-decisions.md)

 新しいプロジェクトの種類を作成する前に行う必要がある項目、プロジェクト ファイルの永続性、およびコミットメントの設計の決定について説明します。

- [チェックリスト: 新しいプロジェクトの種類を作成する](../../extensibility/internals/checklist-creating-new-project-types.md)

 コードの編集や、プロジェクトでのアプリケーションのビルド、デバッグ、配置などのプログラミング タスクをサポートする新しいプロジェクトの種類を作成する場合に従う必要がある手順の概要を示します。

- [プロジェクト ファクトリを使用してプロジェクト インスタンスを作成する](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 プロジェクト ファクトリを提供および使用して新しいプロジェクトのインスタンスを作成する方法について説明します。

- [プロジェクト タイプの登録](../../extensibility/internals/registering-a-project-type.md)

 既定のパスとデータを提供するレジストリからのステートメントのコード サンプル、および各ステートメントのレジストリ スクリプトからのエントリを含むテーブルを示します。

- [プロジェクトの永続性](../../extensibility/internals/project-persistence.md)

 ファイル ベースの`IPersistFileFormat`プロジェクト オブジェクトと非ファイル ベースのプロジェクト オブジェクトの両方を永続化する場合の使用について説明します。

- [MSBuild の使用](../../extensibility/internals/using-msbuild.md)

 プロジェクトの種類でビルド エンジンを使用[!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)]して、ユーザーがコマンド ライン[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]からビルドを実行できるようにする方法について説明します。

## <a name="related-sections"></a>関連項目
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 **オブジェクト ブラウザー**や**クラス ビュー**ウィンドウなどのコード表示ツールのアーキテクチャについて説明します。 VSPackage でオブジェクトの参照を実装するために使用されるインターフェイスとメソッドについて説明します。

- [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)

 プロジェクト項目を開くときにどのエディターを使用するかを決定する際にプロジェクトが果たす重要性と、プロジェクトリソースの操作方法について説明します。

- [Windows インストーラーを使用して VS パッケージをインストールする](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 VSPackage 独自の一意の ID を与える方法と、VSPackage DLL とその他の情報を Windows インストーラー パッケージ (*.MSI*ファイル) を使用して、お客様に展開します。

- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)

 ビューとアドレス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]階層のしくみについて説明します。

- [VSPackages](../../extensibility/internals/vspackages.md)

 環境を拡張するインストール可能な COM オブジェクトである VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の概要を示し、独自の VSPackage を実装する方法について説明します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 プロジェクトを使用してコードの変更、コードのコンパイルとビルド、コードの実行とデバッグを行う方法について説明し、プロジェクトの種類の作成方法に関する詳細なトピックへのリンクを示します。
