---
title: プロジェクトタイプの要点 |マイクロソフトドキュメント
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
ms.openlocfilehash: b44da532207668d9526aec0ccdcab027b94184e6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706379"
---
# <a name="project-type-essentials"></a>プロジェクト タイプの基本情報
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]には、 や[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]などの言語用のいくつかのプロジェクトの種類が含まれています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]また、独自のプロジェクトタイプを作成することもできます。

 カスタム コマンド、エディター、またはツール ウィンドウを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]に追加するだけの場合は、新しいプロジェクトの種類を作成せずに追加できます。 詳細については、次のトピックを参照してください。

- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

- [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)

- [ツール ウィンドウの拡張とカスタマイズ](../../extensibility/extending-and-customizing-tool-windows.md)

  同様に、指定された[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]プロジェクトタイプと[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]プロジェクトタイプの動作をカスタマイズする場合は、プロジェクトのサブタイプを使用して行うことができます。 詳細については、「[プロジェクト のサブタイプ](../../extensibility/internals/project-subtypes.md)」を参照してください。

  次の言語以外の言語に基づくプロジェクト[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]の[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]新しいプロジェクトの種類を作成する必要があります。

- ビルド

- デプロイ

- 複数の構成

- ソース管理

- デバッグ

- ソリューション エクスプローラーのプロジェクト項目

- [**プロジェクトを開く**] ダイアログ ボックスまたは **[新しいプロジェクト**] ダイアログ ボックス

- プロジェクトの入れ子

- プロジェクトの種類の機能の詳細については、次を参照してください。

- プロジェクトの種類は、期待されるインターフェイス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のセットを実装する VSPackage 内のオブジェクトです。 C# を使用してプロジェクトの種類を開発する場合、マネージ パッケージ フレームワーク プロジェクト クラスは必要なインターフェイスを実装し、その実装を継承できます。 詳細については、「[マネージ パッケージ フレームワークを使用したプロジェクトの種類の実装 (C#)」](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)を参照してください。

- C++ 開発者の場合、HierUtil ライブラリのクラスも同様の方法で動作します。 詳細については、「[ビルドにない : HierUtil7 プロジェクト クラスを使用したプロジェクトの種類の実装 (C++)」](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)を参照してください。

- プロジェクトの種類は、.exe または .dll アセンブリにビルドされる一般的なソース コード ファイル以外のデータをサポートできます。 たとえば、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]データベース プロジェクトには、ディスクに格納されているスクリプト ファイルとクエリ ファイルへの参照が含まれ、データベースに対してスクリプトとクエリを実行するコマンドを**ソリューション エクスプローラ**に追加しますが、プロジェクトはビルド動作をサポートしていません。 詳細については、「[プロジェクト項目を開くおよび保存](../../extensibility/internals/opening-and-saving-project-items.md)する 」を参照してください。

- プロジェクトタイプは、ファイルをまったく使用する必要はありません。 たとえば、プロジェクトの種類では、そのすべてのデータをデータベースに格納できます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトの種類は、プロジェクトとプロジェクト項目のデータを保持する方法を完全に制御します。 詳細については、「[プロジェクトの種類の設計に関する決定](../../extensibility/internals/project-type-design-decisions.md)」を参照してください。

- プロジェクトの種類は *、プロジェクト*の種類に基づいてプロジェクトを開くか作成するように指定されたときに[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、プロジェクトの種類のインスタンスを作成するオブジェクトであるプロジェクト ファクトリ を提供する必要があります。 詳細については、「[プロジェクト ファクトリを使用したプロジェクト インスタンスの作成](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)」を参照してください。

- プロジェクトタイプは、プロジェクトおよびプロジェクト項目のテンプレートを提供する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、ユーザーが新しいプロジェクトを作成し、既存のプロジェクトに新しい項目を追加するときにテンプレートが使用されます。 詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

- プロジェクトの種類は、デバッグやリリースなどの複数の構成をサポートできます。 ユーザーは、指定したプロパティ ページを使用して、プロジェクトのさまざまな構成を変更できます。 詳細については、「[構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [プロジェクト タイプの配置](../../extensibility/internals/deploying-project-types.md)
