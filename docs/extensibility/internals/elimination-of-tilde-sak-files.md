---
title: ~SAK ファイルの除去 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0294198bb1560f8df6f17170013f88d4fe11e5cf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708499"
---
# <a name="elimination-of-sak-files"></a>~SAK ファイルの削除
ソース管理プラグイン API 1.2 では、ソース管理プラグインが*MSSCCPRJ*ファイルと共有チェックアウトをサポートするかどうかを検出する機能フラグと新しい関数に *、~SAK*ファイルが置き換えられました。

## <a name="sak-files"></a>~SAK ファイル
Visual Studio .NET 2003 では、*プレフィックスとして "~SAK"* という一時ファイルが作成されました。 これらのファイルは、ソース管理プラグインがサポートするかどうかを判断するために使用されます。

- *ファイル*。

- 複数の(共有)チェックアウト。

ソース管理プラグイン API 1.2 で提供される高度な機能をサポートするプラグインの IDE では、新しい機能、フラグ、および関数を使用して一時ファイルを作成せずに、これらの機能を検出できます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 ソース管理プラグインが複数の (共有) チェックアウトをサポートしている場合は、機能を`SCC_CAP_MULTICHECKOUT`宣言し、関数を`SccIsMultiCheckOutEnabled`実装します。 この関数は、ソース管理されたプロジェクトのいずれかでチェックアウト操作が発生するたびに呼び出されます。

 ソース管理プラグインが*MSSCCPRJ.SCC*ファイルの作成と使用をサポートしている場合は、その機能を`SCC_CAP_SCCFILE`宣言し[、SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)を実装します。 この関数は、ファイルのリストとともに呼び出されます。 この関数は`TRUE' or 'FALSE`、各ファイルに対して、Visual Studio が*MSSCCPRJ.SCC*ファイルを使用するかどうかを示す値を返します。 ソース管理プラグインがこれらの新しい機能をサポートしないことを選択した場合は、次のレジストリ キーを使用してこれらのファイルの作成を無効にすることができます。

 **[HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\8.0\ソースコントロール]一時ファイルを作成しません。** = *dword:00000001*

> [!NOTE]
> このレジストリ キーが*dword:0000000*に設定されている場合は、存在しないキーと同じになり、Visual Studio は一時ファイルを作成しようとします。 ただし、レジストリ キーが*dword:00000001*に設定されている場合、Visual Studio は一時ファイルを作成しません。 代わりに、ソース管理プラグインが*MSSCCPRJ.SCC*ファイルをサポートしておらず、共有チェックアウトをサポートしていないと仮定します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
