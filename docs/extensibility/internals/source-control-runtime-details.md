---
title: ソース管理のランタイムの詳細 |Microsoft Docs
description: プロジェクトをソース管理に追加する方法について説明します。ユーザーがファイルをソース管理のプロジェクトに追加した場合、またはオートメーションコントローラーを使用した場合のいずれかになります。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: bbe1e0e915a28412fcfd411e72b6d622e065b8f8
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877976"
---
# <a name="source-control-runtime-details"></a>ソース管理ランタイムの詳細
プロジェクトは、ユーザーがプロジェクト内のファイルをソース管理に追加するとき、またはウィザードなどのオートメーションコントローラーを介して追加されるときに、ソース管理に追加されます。 プロジェクトは、それ自体がソース管理下にあることを指定していません。ソース管理はサポートされていますが、手動で追加する必要があります。

## <a name="registering-with-a-source-control-package"></a>ソース管理パッケージへの登録
 プロジェクト内のファイルがソース管理に追加されると、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> を呼び出して、ソース管理システムによって cookie として使用される4つの不透明な文字列を提供します。 これらの文字列をプロジェクトファイルに格納します。 これらの文字列は、を呼び出すことによって、プロジェクトタイプのスタートアップ時にソース管理スタブ (ソース管理パッケージを管理する Visual Studio コンポーネント) に渡される必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A> ます。 次に、適切なソース管理パッケージを読み込み、の実装に呼び出しを転送し `IVsSccManager2::RegisterSccProject` ます。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>
- [ソース管理のサポート](../../extensibility/internals/supporting-source-control.md)
