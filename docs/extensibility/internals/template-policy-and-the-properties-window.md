---
title: テンプレート ポリシーとプロパティ ウィンドウ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 08ed6f416441d06767661e63b5e32454dbe07f93
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704662"
---
# <a name="template-policy-and-the-properties-window"></a>テンプレート ポリシーとプロパティ ウィンドウ
エンタープライズ テンプレート プロジェクト内にプロジェクトが含まれている場合、そのエンタープライズ テンプレート プロジェクトはポリシーを適用できます。 テンプレート ポリシーは、プロパティの既定値の設定、プロパティの非表示、プロパティの追加などの制限システムになります。

 テンプレート ポリシーを使用して**プロパティ**ウィンドウの情報の表示を制御する方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>は、実装とは異なります。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>コンポーネント レベルでオブジェクト プロパティを処理し、テンプレート ポリシーを使用してソリューション レベルまたはプロジェクト レベルでオブジェクト プロパティを制約できます。 要するにあの

- メソッドを実装して<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>、特定のオブジェクトの **[プロパティ]** ウィンドウに表示される内容を確認します。

- ソリューション レベルとプロジェクト レベルでテンプレート ポリシーを使用して、以前に指定したオブジェクトの **[プロパティ**] ウィンドウに表示される内容を決定します。

  **ソリューション エクスプローラー**で指定した種類のプロジェクト項目が選択されたときに、テンプレート ポリシーを使用して [**プロパティ]** ウィンドウの特定のプロパティを選択的に制約することは、プロジェクトで作業している開発チームのすべてのメンバーにとって有益です。 たとえば、テンプレート ポリシーを使用して、開発者用にデータベース内のすべての接続文字列情報を設定し、接続文字列を読み取り専用にすることができます。 このようにして、各開発者がデータ アクセスに正しいパスを使用することを保証する簡単な方法を提供できます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
