---
title: ~ SAK Files | の削除Microsoft Docs
description: ソース管理プラグイン API 1.2 からの ~ SAK ファイルの削除、およびそれらのファイルが機能フラグと新しい関数にどのように置き換えられたかについて説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 8e846354b2d48b2f7866daa14987e757f41779c8
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480513"
---
# <a name="elimination-of-sak-files"></a>~ SAK ファイルの削除
ソース管理プラグイン API 1.2 では、 *~ SAK* ファイルは機能フラグと、ソース管理プラグインが *mssccprj.scc* ファイルと共有チェックアウトをサポートしているかどうかを検出する新しい関数に置き換えられています。

## <a name="sak-files"></a>~ SAK ファイル
Visual Studio .NET 2003 では、 *~ SAK* で始まる一時ファイルが作成されました。 これらのファイルは、ソース管理プラグインが以下をサポートしているかどうかを判断するために使用されます。

- *Mssccprj.scc* ファイル。

- 複数の (共有) チェックアウト。

ソース管理プラグイン API 1.2 で提供される高度な機能をサポートするプラグインの場合、IDE は、次のセクションで詳しく説明する新しい機能、フラグ、および関数を使用して、一時ファイルを作成せずにこれらの機能を検出できます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 ソース管理プラグインが複数の (共有) チェックアウトをサポートしている場合は、 `SCC_CAP_MULTICHECKOUT` 機能を宣言し、関数を実装し `SccIsMultiCheckOutEnabled` ます。 この関数は、ソース管理されたプロジェクトのいずれかでチェックアウト操作が行われるたびに呼び出されます。

 ソース管理プラグインが、 *mssccprj.scc* ファイルの作成と使用をサポートしている場合は、機能を宣言し、 `SCC_CAP_SCCFILE` [scc ccfile](../../extensibility/sccwillcreatesccfile-function.md)を実装します。 この関数は、ファイルの一覧を使用して呼び出されます。 関数は、 `TRUE' or 'FALSE` 各ファイルに対してを返し、Visual Studio で *mssccprj.scc* ファイルを使用する必要があるかどうかを示します。 ソース管理プラグインがこれらの新機能と機能をサポートしないことを選択した場合、次のレジストリキーを使用してこれらのファイルの作成を無効にすることができます。

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl**  =  *dword: 00000001*

> [!NOTE]
> このレジストリキーが *dword: 00000000* に設定されている場合は、キーが存在しないことに相当し、Visual Studio は一時ファイルの作成を試みます。 ただし、レジストリキーが *dword: 00000001* に設定されている場合、Visual Studio は一時ファイルを作成しません。 代わりに、ソース管理プラグインが *mssccprj.scc* ファイルをサポートしておらず、共有チェックアウトをサポートしていないことを前提としています。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
