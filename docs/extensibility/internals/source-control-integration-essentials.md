---
title: ソース管理統合の基礎 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e56658d644720f1563d71d3d08bf35268119112f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705233"
---
# <a name="source-control-integration-essentials"></a>ソース管理の統合の基本情報
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]基本的な機能を提供し、ソース管理プラグイン API (旧 MSSCCI API) を使用してビルドされるソース管理プラグインと、より堅牢な機能を提供する VSPackage ベースのソース管理統合ソリューションの 2 種類のソース管理統合がサポートされています。

## <a name="source-control-plug-in"></a>ソース管理プラグイン
 ソース管理プラグインは、ソース管理プラグイン API を実装する DLL として記述されます。 登録とソース管理の統合機能は、API を通じて提供されます。 この方法は、ソース管理の VSPackage よりも実装が簡単で、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ほとんどのソース管理操作にユーザー インターフェイス (UI) を使用します。

 ソース管理プラグイン API を使用してソース管理プラグインを実装するには、次の手順を実行します。

1. [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)で指定された関数を実装する DLL を作成します。

2. [「方法 : ソース管理プラグインをインストールする](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)」の説明に従って、適切なレジストリ エントリを作成して DLL を登録します。

3. ヘルパー UI を作成し、ソース管理アダプター パッケージ (ソース管理プラグイン[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を通じてソース管理機能を処理するコンポーネント) によって要求されたときに表示します。

   詳細については、「[ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)」を参照してください。

## <a name="source-control-vspackage"></a>ソース管理 VS パッケージ
 ソース管理の VSPackage 実装を使用すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理 UI のカスタマイズされた置き換えを開発できます。 この方法では、ソース管理の統合を完全に制御できますが、UI 要素を提供し、プラグインのアプローチで提供されるソース管理インターフェイスを実装する必要があります。

 ソース管理の VSPackage を実装するには、次の操作を行う必要があります。

1. 登録と選択 の説明に従って、独自のソース管理 VSPackage を作成[して登録](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)します。

2. 既定のソース管理 UI をカスタム UI に置き換えます。 [「カスタム ユーザー インターフェイス](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)」を参照してください。

3. 使用するグリフを指定し、ソリューション**エクスプローラー**のグリフ イベントを処理します。 [「グリフ コントロール](../../extensibility/internals/glyph-control-source-control-vspackage.md)」を参照してください。

4. クエリ編集イベントおよびクエリの保存イベントの処理 ([クエリ編集クエリの保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)に示すように)

   詳細については、「[ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [概要](../../extensibility/internals/source-control-integration-overview.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [ソース管理 VSPackage の作成](../../extensibility/internals/creating-a-source-control-vspackage.md)
