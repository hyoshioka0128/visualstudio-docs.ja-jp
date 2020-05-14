---
title: ソース管理ランタイムの詳細 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 92ce5e822ec7360b3b1a4010d250a4349443c142
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705037"
---
# <a name="source-control-runtime-details"></a>ソース管理ランタイムの詳細
ユーザーがプロジェクト内のファイルをソース管理に追加するとき、またはウィザードなどのオートメーション コントローラーを使用してプロジェクトがソース管理に追加されます。 プロジェクトは、ソース管理下にあることをそれ自体に指定しません。ソース管理をサポートしていますが、手動で追加する必要があります。

## <a name="registering-with-a-source-control-package"></a>ソース管理パッケージへの登録
 プロジェクト内のファイルがソース管理に追加されると、環境は、ソース<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>管理システムによって Cookie として使用される 4 つの不透明な文字列を提供する呼び出しします。 これらの文字列をプロジェクト ファイルに格納します。 これらの文字列は、プロジェクトの種類の起動時にソース管理スタブ (ソース管理パッケージを管理する Visual Studio コンポーネント) に<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>渡す必要があります。 これにより、適切なソース管理パッケージが読み込まれ、呼び出しが`IVsSccManager2::RegisterSccProject`の実装に転送されます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
