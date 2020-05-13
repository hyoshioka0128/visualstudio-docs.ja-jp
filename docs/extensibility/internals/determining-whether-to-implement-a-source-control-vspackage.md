---
title: ソース管理 VSPackage を実装するかどうかを決定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8707f3c1ced1cc2df9d3ae77280fc8779874a837
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708722"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>ソース管理 VSPackage を実装するかどうかを決定します。
このセクションでは、ソース管理ソリューションを拡張するためのソース管理プラグインとソース管理 VSPackages の選択肢について詳しく説明し、適切な統合パスの選択に関する広範なガイドラインを示します。

## <a name="small-source-control-solution-with-limited-resources"></a>リソースが限られた小規模なソース管理ソリューション
 リソースが限られており、ソース管理パッケージを作成するオーバーヘッドを負担できない場合は、ソース管理プラグイン API ベースのプラグインを作成できます。 詳細については、[登録と選択を](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)参照してください。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>豊富な機能セットを備えた大規模なソース管理ソリューション
 ソース管理プラグイン API を使用して適切にキャプチャされていない、豊富なソース管理モデルを提供するソース管理ソリューションを実装する場合は、ソース管理パッケージを統合パスと見なすことができます。 これは、ソース管理アダプター パッケージ (ソース管理プラグインと通信し、基本的なソース管理 UI を提供する) を独自の方法で処理できるように、独自のソース管理アダプター パッケージを置き換える場合に特に当てはまります。 既に満足のいくソース管理 UI を使用していて、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]でのそのエクスペリエンスを保持する場合は、ソース管理パッケージ オプションを使用して、その操作を行うことができます。 ソース管理パッケージは汎用的なものではなく、IDE で[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用するためだけに設計されています。

 ソース管理ロジックと UI を柔軟かつ詳細に制御できるソース管理ソリューションを実装する場合は、ソース管理パッケージの統合ルートを使用する方がよい場合があります。 次のようにすることができます。

1. 独自のソース管理 VSPackage を登録します ([登録と選択](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)を参照)。

2. 既定のソース管理 UI をカスタム UI に置き換えます (「[カスタム ユーザー インターフェイス](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)」を参照)。

3. 使用するグリフを指定し、ソリューション エクスプローラのグリフ イベントを処理します[(Glyph コントロール](../../extensibility/internals/glyph-control-source-control-vspackage.md)を参照)。

4. クエリ編集イベントおよびクエリ保存イベントの処理 (「[クエリ編集クエリの保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)」を参照)。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインを作成する](../../extensibility/internals/creating-a-source-control-plug-in.md)
