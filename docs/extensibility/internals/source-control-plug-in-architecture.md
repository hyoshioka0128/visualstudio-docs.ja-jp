---
title: ソース管理プラグインのアーキテクチャ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f549ad2c4ee456860a08fbf20ccda813934a8582
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705109"
---
# <a name="source-control-plug-in-architecture"></a>アーキテクチャのソース管理プラグイン
ソース管理プラグインを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]実装およびアタッチすることで、統合開発環境 (IDE) にソース管理サポートを追加できます。 IDE は、明確に定義されたソース管理プラグイン API を介してソース管理プラグインに接続します。 IDE は、ツール バーとメニュー コマンドで構成されるユーザー インターフェイス (UI) を提供することで、ソース管理システムのバージョン管理機能を公開します。 ソース管理プラグインは、ソース管理機能を実装します。

## <a name="source-control-plug-in-resources"></a>ソース管理プラグイン リソース
 ソース管理プラグインは、バージョン管理アプリケーションを作成して IDE に接続するためのリソースを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供します。 ソース管理プラグインには、IDE に統合できるようにソース管理プラグインによって実装する必要がある API 仕様が[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]含まれています。 また、ソース管理プラグイン API に準拠した必須関数の実装を示すスケルトン ソース管理プラグインを実装するコード サンプル (C++ で記述) も含まれています。

 ソース管理プラグイン API 仕様では、ソース管理プラグイン API に従って実装された関数の必須セットを使用してソース管理 DLL を作成する場合に、任意のソース管理システムを利用できます。

## <a name="components"></a>Components
 図のソース管理アダプター パッケージは、ソース管理プラグインでサポートされる関数呼び出しにソース管理操作のユーザーの要求を変換する IDE のコンポーネントです。 これを実現するには、IDE とソース管理プラグインに、IDE とプラグインの間で情報をやり取りする有効なダイアログが必要です。 このダイアログを行うには、両方とも同じ言語を話す必要があります。 このドキュメントで説明するソース管理プラグイン API は、この交換の一般的な語彙です。

 ![ソース コード管理アーキテクチャ図](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch")VS とソース管理プラグインの相互作用を示すアーキテクチャ図

 アーキテクチャ図に示すように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]図の中で VS シェルとしてラベル付けされたシェルは、エディターやソリューション エクスプローラーなどのユーザーの作業プロジェクトと関連コンポーネントをホストします。 ソース管理アダプター パッケージは、IDE とソース管理プラグインの間の対話を処理します。 ソース管理アダプター パッケージには、独自のソース管理 UI が用意されています。 これは、ソース管理操作のスコープを開始および定義するためにユーザーが操作するトップレベル UI です。

 ソース管理プラグインは独自の UI を持つことができます。 "ベンダー UI" というラベルのボックスは、ソース管理プラグイン作成者として提供するカスタム ユーザー インターフェイス要素を表します。 これらは、ユーザーが高度なソース管理操作を呼び出したときに、ソース管理プラグインによって直接表示されます。 "ヘルパー UI" というラベルのボックスは、IDE を通じて間接的に呼び出されるソース管理プラグイン UI 機能のセットです。 ソース管理プラグインは、IDE によって提供される特別なコールバック関数を通じて、UI 関連のメッセージを IDE に渡します。 ヘルパー UI は、IDE とのシームレスな統合を容易にし (多くの場合、**高度な**ボタンを使用して)、より統一されたエンドユーザーエクスペリエンスを提供します。

 ソース管理プラグインは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、シェルに変更を加え、その結果、ソース管理アダプター パッケージまたは IDE によって提供されるソース管理 UI に変更を加えることはできません。 エンド ユーザーの統合エクスペリエンスに貢献するさまざまなソース管理プラグイン API 関数の実装によって提供される柔軟性を最大限に活用する必要があります。 ソース管理プラグイン API ドキュメントのリファレンス セクションには、いくつかの高度なソース管理プラグイン機能の情報が含まれています。 これらの機能を利用するには、ソース管理プラグインは初期化中に IDE に高度な機能を宣言し、各機能に対して特定の高度な機能を実装する必要があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)
- [用語集](../../extensibility/source-control-plug-in-glossary.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
