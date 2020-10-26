---
title: プロジェクトの種類の要点 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b7634802899d72eb6abcb0aa837b8fb6a532b966
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012062"
---
# <a name="project-type-essentials"></a>プロジェクト タイプの基本情報
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、やなどの言語用のプロジェクトの種類がいくつか含まれてい [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、独自のプロジェクトの種類を作成することもできます。

 カスタムコマンド、エディター、またはツールウィンドウをに追加するだけの場合は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、新しいプロジェクトの種類を作成しなくてもかまいません。 詳細については、次のトピックを参照してください。

- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

- [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)

- [ツール ウィンドウの拡張とカスタマイズ](../../extensibility/extending-and-customizing-tool-windows.md)

  同様に、指定されたおよびプロジェクトの種類の動作をカスタマイズする場合は、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] プロジェクトのサブタイプを使用します。 詳細については、「 [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

  [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 次の1つまたは複数をサポートする場合は、以外の言語に基づくプロジェクトの新しいプロジェクトの種類を作成する必要があります。

- Build

- デプロイ

- 複数の構成

- ソース管理

- デバッグ

- ソリューションエクスプローラー内のプロジェクト項目

- [ **プロジェクトを開く** ] または [ **新しいプロジェクト** ] ダイアログボックス

- プロジェクトの入れ子

- プロジェクトの種類の機能の詳細については、以下を参照してください。

- プロジェクトの種類は、に必要な一連のインターフェイスを実装する VSPackage 内のオブジェクトです [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 C# を使用してプロジェクトの種類を開発している場合は、マネージパッケージフレームワークプロジェクトクラスによって必要なインターフェイスが実装され、その実装を継承できるようになります。 詳細については、「 [マネージパッケージフレームワークを使用したプロジェクトの種類の実装 (C#)](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)」を参照してください。

- C++ 開発者にとって、HierUtil ライブラリのクラスは同様の方法で動作します。 詳細については、「 [ビルド内にありません: HierUtil7 プロジェクトクラスを使用したプロジェクトの種類の実装 (C++)](/previous-versions/bb166212(v=vs.100))」を参照してください。

- プロジェクトの種類では、.exe または .dll アセンブリに組み込まれている一般的なソースコードファイル以外のデータをサポートできます。 たとえば、データベースプロジェクトには、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ディスクに格納されているスクリプトおよびクエリファイルへの参照が含まれています。また、データベースに対してスクリプトとクエリを実行するために **ソリューションエクスプローラー** にコマンドを追加していますが、プロジェクトでビルド動作がサポートされていません。 詳細については、「 [プロジェクト項目を開いて保存](../../extensibility/internals/opening-and-saving-project-items.md)する」を参照してください。

- プロジェクトの種類では、ファイルを使用する必要はありません。 たとえば、プロジェクトの種類では、すべてのデータをデータベースに格納できます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトの種類により、プロジェクトおよびプロジェクト項目のデータを永続化する方法を完全に制御できます。 詳細については、「 [プロジェクトの種類の設計](../../extensibility/internals/project-type-design-decisions.md)上の決定」を参照してください。

- プロジェクトの種類はプロジェクト *ファクトリ*を提供する必要があります。これは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がプロジェクトの種類に基づいてプロジェクトを開くか作成するように指示されるたびに、プロジェクトの種類のインスタンスを作成するオブジェクトです。 詳細については、「 [プロジェクトファクトリを使用したプロジェクトインスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。

- プロジェクトの種類では、プロジェクトおよびプロジェクト項目のテンプレートを指定する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、ユーザーが新しいプロジェクトを作成し、既存のプロジェクトに新しい項目を追加するときに、テンプレートが使用されます。 詳細については、「 [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

- プロジェクトの種類では、デバッグやリリースなどの複数の構成をサポートできます。 ユーザーは、指定したプロパティページを使用して、プロジェクトのさまざまな構成を変更できます。 詳細については、「 [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)