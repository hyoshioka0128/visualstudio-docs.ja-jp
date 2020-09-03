---
title: プロジェクトの種類を作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bbe65d1615603e4dc7546dbfe3530093c62528e5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155031"
---
# <a name="creating-project-types"></a>プロジェクト タイプの作成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

を拡張する [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] には、新しいプロジェクトの種類を作成します。 新しいプロジェクトの種類を作成するには、いくつかの概念を理解し、いくつかの手順を完了する必要があります。 次のトピックでは、プロジェクトの種類を作成する方法の概要について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [プロジェクト タイプのデザインの方針](../../extensibility/internals/project-type-design-decisions.md)  
 新しいプロジェクトの種類を作成する前に行う必要がある項目、プロジェクトファイルの永続化、およびコミットメント整備士の設計上の決定について説明します。  
  
 [チェックリスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)  
 コードの編集、プロジェクトでのアプリケーションのコンパイル、ビルド、デバッグ、および配置としてのプログラミングタスクをサポートする新しいプロジェクトの種類を作成するために従う必要がある手順の概要について説明します。  
  
 [プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)  
 プロジェクトファクトリを提供および使用して、新しいプロジェクトのインスタンスを作成する方法について説明します。  
  
 [プロジェクト タイプの登録](../../extensibility/internals/registering-a-project-type.md)  
 既定のパスとデータを提供するレジストリのステートメントのコードサンプルと、各ステートメントのレジストリスクリプトのエントリを含むテーブルを提供します。  
  
 [プロジェクトの永続化](../../extensibility/internals/project-persistence.md)  
 の使用方法について説明し `IPersistFileFormat` ます。これにより、ファイルベースのプロジェクトオブジェクトとファイルベースでないプロジェクトオブジェクトの両方が保持されます。  
  
 [MSBuild の使用](../../extensibility/internals/using-msbuild.md)  
 プロジェクトの種類でビルドエンジンを使用して [!INCLUDE[vstecmsbuild](../../includes/vstecmsbuild-md.md)] 、ユーザーがコマンドラインからビルドできるようにする方法について説明し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
## <a name="related-sections"></a>関連項目  
 [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)  
 **オブジェクトブラウザー**や**クラスビュー**ウィンドウなどのコード表示ツールのアーキテクチャについて説明します。 VSPackage でオブジェクトの参照を実装するために使用されるインターフェイスとメソッドについて説明します。  
  
 [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)  
 プロジェクト項目が開かれたときにどのエディターを使用するか、およびプロジェクトリソースを操作する方法を決定するときに、プロジェクトが果たす意味について説明します。  
  
 [Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)  
 VSPackage に独自の一意の id を与える方法と、VSPackage Dll やその他の情報を Windows インストーラーパッケージ () にラップする方法を示します。MSI ファイル) をお客様に展開できます。  
  
 [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ビューとアドレスの階層について説明します。  
  
 [VSPackages](../../extensibility/internals/vspackages.md)  
 VSPackage の概要、環境を拡張するインストール可能な COM オブジェクト、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 独自の VSPackage の実装方法について説明します。  
  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 プロジェクトを使用してコードの変更、コードのコンパイルとビルド、コードの実行とデバッグを行う方法について説明します。また、プロジェクトの種類の作成方法に関する詳細なトピックへのリンクも示します。
