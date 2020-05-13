---
title: 構文の色分けの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax coloring, implementing
- editors [Visual Studio SDK], colorizing text
- text, colorizing in editors
ms.assetid: 96e762ca-efd0-41e7-8958-fda4897c8c7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83ce66dd6a31e3ef852feb91e2ba304e6688a723
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707642"
---
# <a name="implementing-syntax-coloring"></a>構文の色分け表示の実装
言語サービスが構文の色付けを提供する場合、パーサーはテキスト行を色分け可能な項目の配列に変換し、これらの色付け可能な項目に対応するトークン型を返します。 パーサーは、色付きの項目のリストに属するトークン型を返す必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Colorizer オブジェクトによって適切なトークンタイプに割り当てられた属性に従って、コードウィンドウに各カラーリング可能な項目が表示されます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]パーサー インターフェイスを指定する必要はありませんし、パーサーの実装は完全にユーザーに対して行われます。 ただし、既定のパーサーの実装は Visual Studio 言語パッケージ プロジェクトで提供されます。 マネージ コードの場合、マネージ パッケージ フレームワーク (MPF) は、テキストの色分けを完全にサポートします。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 構文の色分けを実装する新しい方法の詳細については、「[チュートリアル: テキストの強調表示](../../extensibility/walkthrough-highlighting-text.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="steps-followed-by-an-editor-to-colorize-text"></a>テキストを色分けするエディタの手順

1. エディターは、オブジェクトのメソッドを呼び<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo.GetColorizer%2A>出すことによって、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageInfo>カラー化ツールを取得します。

2. エディターは、カラー<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStateMaintenanceFlag%2A>化器の外側に維持される各行の状態を必要とするかどうかを判断するメソッドを呼び出します。

3. カラー化器の外側で状態を維持する必要がある場合、エディターはメソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.GetStartState%2A>呼び出して最初の行の状態を取得します。

4. バッファー内の各行について、エディターはメソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>呼び出し、次の手順を実行します。

    1. テキスト行は、テキストをトークンに変換するためにスキャナーに渡されます。 各トークンは、トークンテキストとトークンタイプを指定します。

    2. トークンの種類は、インデックスに変換され、色付け可能な項目リストに変換されます。

    3. トークン情報は、配列の各要素が行内の文字に対応するように配列を埋めるために使用されます。 配列に格納されている値は、色付け可能な項目リストのインデックスです。

    4. 行の終わりの状態は、各行に対して返されます。

5. カラー化装置が状態を維持する必要がある場合、エディターはその行の状態をキャッシュします。

6. エディターは、メソッドから返された情報を使用してテキスト行を<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer.ColorizeLine%2A>レンダリングします。 この場合、次の手順が必要です。

    1. 行の各文字について、色分け可能な項目のインデックスを取得します。

    2. 既定の色付け可能なアイテムを使用している場合は、エディターの色指定可能な項目リストにアクセスします。

    3. それ以外の場合は、言語サービス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems.GetColorableItem%2A>のメソッドを呼び出して、色分け可能な項目を取得します。

    4. カラー設定可能アイテムの情報を使用して、テキストを表示します。

## <a name="managed-package-framework-colorizer"></a>管理パッケージ フレームワーク の色付け
 マネージ パッケージ フレームワーク (MPF) は、カラー化プログラムの実装に必要なすべてのクラスを提供します。 言語サービス クラスは、クラス<xref:Microsoft.VisualStudio.Package.LanguageService>を継承し、必要なメソッドを実装する必要があります。 インターフェイスを実装してスキャナーとパーサーを<xref:Microsoft.VisualStudio.Package.IScanner>指定し、<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>そのインターフェイスのインスタンスをメソッド (<xref:Microsoft.VisualStudio.Package.LanguageService>クラスに実装する必要があるメソッドの 1 つ) から返す必要があります。 詳細については、「[従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: ビルトインの配色可能な項目の使用](../../extensibility/internals/how-to-use-built-in-colorable-items.md)
- [カスタムの配色可能な項目](../../extensibility/internals/custom-colorable-items.md)
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
