---
title: テンプレートポリシーと [プロパティ] ウィンドウ |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704662"
---
# <a name="template-policy-and-the-properties-window"></a>テンプレート ポリシーとプロパティ ウィンドウ
エンタープライズテンプレートプロジェクト内にプロジェクトが含まれている場合、そのエンタープライズテンプレートプロジェクトでポリシーを適用できます。 テンプレートポリシーは、プロパティの既定値を設定したり、プロパティを非表示にしたり、プロパティを追加したりするために使用できる制約システムになります。

 テンプレートポリシーを使用して、[ **プロパティ** ] ウィンドウでの情報の表示を制御することは、の実装とは異なり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> コンポーネントレベルでオブジェクトのプロパティを処理します。テンプレートポリシーを使用して、ソリューションレベルまたはプロジェクトレベルでオブジェクトのプロパティを制約できます。 要するにあの

- にメソッドを実装して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 、特定のオブジェクトの [ **プロパティ** ] ウィンドウに表示される内容を決定します。

- ソリューションおよびプロジェクトレベルでテンプレートポリシーを使用して、以前に指定したオブジェクトの [ **プロパティ** ] ウィンドウに表示される内容を決定します。

  テンプレートポリシーを使用して、指定された種類のプロジェクト項目が**ソリューションエクスプローラー**で選択されている場合に、[**プロパティ**] ウィンドウで特定のプロパティを選択的に制限することができます。これは、プロジェクトで作業している開発チームのすべてのメンバーに役立ちます。 たとえば、テンプレートポリシーを使用すると、開発者がデータベース内のすべての接続文字列情報を設定し、接続文字列を読み取り専用にすることができます。 このようにして、各開発者がデータアクセスに適切なパスを使用するようにするための簡単な方法を提供できます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>
- [プロパティの拡張](../../extensibility/internals/extending-properties.md)
