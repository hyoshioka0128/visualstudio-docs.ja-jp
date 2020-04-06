---
title: ソース管理統合の概要 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d80363286f5f0cac9a5ceb2e8ac9d20345df9e6f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705121"
---
# <a name="source-control-integration-overview"></a>ソース管理の統合の概要
このセクションでは、Visual Studio ソース管理に統合する 2 つの方法を比較します。ソース管理プラグインと、ソース管理ソリューションを提供し、新しいソース管理機能を強調表示する VSPackage。 Visual Studio では、ソース管理 VSPackages とソース管理プラグインの間で手動で切り替えるだけでなく、ソリューション ベースの自動切り替えもできます。

## <a name="source-control-integration"></a>ソース管理の統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、2 種類のソース管理統合オプションがサポートされています。 の全バージョンでは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、Visual Studio ソース管理ユーザー インターフェイス (UI) を使用しながら基本的なソース管理機能を提供するソース管理プラグイン API (以前は MSSCCI API とも呼ばれていた) に基づくプラグインを統合できます。 一方、ソース管理 VSPackage は、ソース管理モデルで高度な高度[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]化と自律性を要求するソース管理統合に適した、新しい深い統合パスを提供します。

 ![ソース管理の概要](../../extensibility/internals/media/sourcectnrloverview.gif "概要")

## <a name="source-control-plug-in"></a>ソース管理プラグイン
 Visual Studio のすべてのバージョンでは、ソース管理プラグイン API 仕様バージョン 1.2 を統合パスとしてサポートしています。 ソース管理プラグインの実装者は、ソース管理プラグインの作成で説明されているように、ソース管理プラグインの統合と登録のためのソース[管理プラグイン](../../extensibility/internals/creating-a-source-control-plug-in.md)API 関数を実装する DLL を書き込みます。 この方法では、統合開発環境 (IDE) は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]チェックイン、チェックアウト、ツール/オプションのプロパティ ページ、ツールバー、ソース管理グリフなどのダイアログ ボックスの UI を使用します。 ソース管理プラグイン API を厳密に準拠させると、Visual Studio への簡単な統合とユーザーのトラブルのないエクスペリエンスが保証されます。 つまり、ソース管理プラグインは、API で詳細に記述されている関数とコールバックのほとんどを実装する必要があります。

 ソース管理プラグイン API を使用してソース管理プラグインを実装するには、次の手順を実行します。

1. [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)で指定された関数を実装する DLL を作成します。

2. 適切なレジストリ エントリを作成して DLL を登録します ([方法: ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)を参照)。

3. ヘルパー UI を作成し、ソース管理アダプター パッケージ (ソース管理プラグインを介してソース管理機能を処理する Visual Studio コンポーネント) によって要求されたときに表示します。

   ソース管理コマンドに応答して、Visual Studio IDE は、基本的な操作の標準 UI を表示し、ソース管理プラグイン API で定義された関数を使用してソース管理プラグインに情報を渡します。 高度なオプションの場合、ソース管理プラグインを呼び出して、ソース管理プロジェクトの参照など、独自の UI を表示できます。 つまり、ソース管理を扱う際に、Visual Studio が提供する UI とソース管理プラグインが提供する UI という 2 つの異なるスタイルの UI がユーザーに提示される可能性があります。 これは、高度なソース管理操作で最も顕著です。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインの実装の欠点

- 高度な機能の場合、ユーザーには 2 種類の異なるインターフェイスが表示され、混乱が生じる可能性があります。

- ソース管理プラグインは、ソース管理プラグイン API によって暗黙のソース管理モデルに限定されます。

- ソース管理プラグイン API は、一部のソース管理シナリオでは制限が厳しすぎる場合があります。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインの実装の利点

- Visual Studio では、すべての基本的なソース管理操作のすべての UI が提供されるため、ソース管理プラグインは、潜在的に複雑な UI を実装する必要はありません。

- 厳密な API により、ソース管理プラグインは外部ソース管理プログラムと容易に対話して、より広範な機能を提供できます。Visual Studio では、ソース管理プラグイン API に従って実行されるだけ、ソース管理機能の実行方法をあまり気にしません。

- ソース管理の VSPackage よりもソース管理プラグインを実装する方が簡単です。

## <a name="source-control-vspackage"></a>ソース管理 VS パッケージ
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]ソース管理機能の完全な制御と Visual Studio 提供のソース管理ユーザー インターフェイスの完全な置き換えと Visual Studio に深い統合を可能にします。 ソース管理の VSPackage は、Visual Studio に登録され、ソース管理機能を提供します。 複数のソース管理 VSPackage を Visual Studio に登録できますが、一度にアクティブにできるのは 1 つだけです。 ソース管理の VSPackage は、Visual Studio のソース管理機能と外観を、アクティブな状態で完全に制御できます。 システムに登録されているその他のソース管理 VSPackages は非アクティブであり、UI をまったく表示しません。

 ソース管理 VSPackage を実装するには、"すべてまたは何も" 戦略が必要です。 ソース管理 VSPackage の作成者は、ソース管理の機能全体をカバーするソース管理インターフェイスと新しい UI 要素 (ダイアログ ボックス、メニュー、およびツール バー) の数を実装するのにかなりの労力を投資する必要があります。 詳細については[、「ソース管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)の作成」を参照してください。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>ソース管理 VSPackage の実装の欠点

- VSPackage は、Visual Studio と正常に統合するために、いくつかの複雑なインターフェイスを実装する必要があります。

- VSPackage は、ソース管理に必要なすべての UI を提供する必要があります。この領域では、Visual Studio ではサポートは提供されません。

- ソース管理 VSPackage は Visual Studio と密接に関連付けられており、スタンドアロン プログラムでは動作できないため、機能をソース管理プログラムの外部バージョンと簡単に共有することはできません。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>ソース管理 VS パッケージを実装する利点

- VSPackage はソース管理の UI と機能を完全に制御するため、ユーザーはソース管理のシームレスなインターフェイスを提供します。

- VSPackage は、特定のソース管理モデルに限定されません。

## <a name="see-also"></a>関連項目
- [ソース管理](../../extensibility/internals/source-control.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [ソース管理の新機能](../../extensibility/internals/what-s-new-in-source-control.md)
