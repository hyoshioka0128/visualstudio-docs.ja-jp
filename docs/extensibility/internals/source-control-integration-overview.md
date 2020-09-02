---
title: ソース管理の統合の概要 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705121"
---
# <a name="source-control-integration-overview"></a>ソース管理の統合の概要
このセクションでは、Visual Studio ソース管理に統合する2つの方法を比較します。ソース管理のプラグインと、ソース管理ソリューションを提供し、新しいソース管理機能を強調する VSPackage。 Visual Studio では、ソース管理 Vspackage とソース管理プラグインを手動で切り替えることができ、ソリューションベースの自動切り替えも可能です。

## <a name="source-control-integration"></a>ソース管理の統合
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、2種類のソース管理統合オプションがサポートされています。 のすべてのバージョンで [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、ソース管理プラグイン API (以前は MSSCCI api とも呼ばれます) に基づいてプラグインを統合できます。これにより、Visual Studio ソース管理のユーザーインターフェイス (UI) を使用しているときに基本的なソース管理機能が提供されます。 一方、ソース管理 VSPackage は、ソース管理 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] モデルの高度なレベルと自律性を要求するソース管理の統合に適した新しい高度な統合パスを提供します。

 ![ソース管理の概要](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>ソース管理プラグイン
 すべてのバージョンの Visual Studio では、統合パスとしてソース管理プラグイン API 仕様バージョン1.2 がサポートされています。 ソース管理プラグインの実装者は、「ソース管理プラグインの [作成](../../extensibility/internals/creating-a-source-control-plug-in.md)」で説明されているように、ソース管理の統合と登録のためにソース管理プラグイン API 関数を実装する DLL を記述します。 この方法では、統合開発環境 (IDE) で、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] チェックイン、チェックアウト、ツール/オプションのプロパティページ、ツールバー、ソース管理のグリフなどのダイアログボックスに UI を使用します。 ソース管理プラグイン API に厳密に準拠することで、Visual Studio との統合が容易になり、ユーザーにとっては問題のないエクスペリエンスを実現できます。 これは、ソース管理プラグインが、API で詳細に説明されている関数とコールバックの大部分を実装する必要があることを意味します。

 ソース管理プラグイン API を使用してソース管理プラグインを実装するには、次の手順を実行します。

1. [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)に指定されている関数を実装する DLL を作成します。

2. 適切なレジストリエントリを作成して、DLL を登録します (「 [方法: ソース管理プラグインをインストール](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)する」を参照してください)。

3. ソース管理アダプターパッケージ (ソース管理プラグインを使用してソース管理機能を処理する Visual Studio コンポーネント) によってプロンプトが表示されたら、ヘルパー UI と表示を作成します。

   ソース管理コマンドに対する応答として、Visual Studio IDE は基本的な操作のための標準 UI を提供し、ソース管理プラグイン API で定義されている関数を使用して、ソース管理プラグインに情報を渡します。 詳細オプションでは、ソース管理プラグインをで呼び出して、ソース管理されたプロジェクトを参照するなど、独自の UI を表示することができます。 これは、ソース管理を扱うときに、Visual Studio によって表示される ui とソース管理プラグインによって提供される UI という2つの異なるスタイルの UI をユーザーに表示できることを意味します。 これは、高度なソース管理操作で最も顕著になります。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装する場合の欠点

- 高度な機能の場合、ユーザーには2つの異なるスタイルのインターフェイスが表示され、混乱を招く可能性があります。

- ソース管理プラグインは、ソース管理プラグイン API によって暗黙的に指定されるソース管理モデルに限定されます。

- ソース管理プラグイン API は、ソース管理のシナリオによっては制限が厳しすぎる可能性があります。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>ソース管理プラグインを実装する利点

- Visual Studio には、ソース管理プラグインが複雑な UI を実装する必要がないように、すべての基本的なソース管理操作の UI が用意されています。

- 厳密な API により、ソース管理プラグインは、より広範な機能を提供するために、外部ソース管理プログラムと簡単にやり取りできます。Visual Studio では、ソース管理の機能がどのように実現されているかは考慮されません。ソース管理プラグイン API によってのみ実現されます。

- ソース管理プラグインは、ソース管理 VSPackage よりも簡単に実装できます。

## <a name="source-control-vspackage"></a>ソース管理 VSPackage
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ソース管理機能を完全に制御し、Visual Studio によって提供されるソース管理ユーザーインターフェイスを完全に置き換えることで、Visual Studio への緊密な統合を可能にします。 ソース管理 VSPackage は、Visual Studio に登録され、ソース管理機能を提供します。 いくつかのソース管理 Vspackage は Visual Studio に登録できますが、一度にアクティブにできるのは1つだけです。 ソース管理 VSPackage は、Visual Studio がアクティブになっている間、ソース管理機能と外観を完全に制御できます。 システムに登録されている可能性のある他のすべてのソース管理 Vspackage は、非アクティブになり、UI がまったく表示されません。

 ソース管理 VSPackage を実装するには、"すべて" または "なし" の戦略が必要です。 ソース管理 VSPackage の作成者は、ソース管理機能全体に対応するために、多数のソース管理インターフェイスと新しい UI 要素 (ダイアログボックス、メニュー、およびツールバー) を実装するために多大な労力を費やす必要があります。 詳細について [は、「ソース管理の作成 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md) 」を参照してください。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>ソース管理を実装する場合の欠点 VSPackage

- VSPackage は、Visual Studio と正常に統合するために、多数の複雑なインターフェイスを実装する必要があります。

- VSPackage は、ソース管理に必要なすべての UI を提供する必要があります。この領域では、Visual Studio によるサポートは提供されません。

- ソース管理 VSPackage は、Visual Studio に関連付けられていて、スタンドアロンプログラムでは動作できないため、ソース管理プログラムの外部バージョンとの間で簡単に共有することはできません。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>ソース管理 VSPackage を実装する利点

- VSPackage はソース管理の UI と機能を完全に制御できるため、ユーザーにはソース管理用のシームレスなインターフェイスが表示されます。

- VSPackage は、特定のソース管理モデルに限定されていません。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理](../../extensibility/internals/source-control.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [ソース管理の新機能](../../extensibility/internals/what-s-new-in-source-control.md)
