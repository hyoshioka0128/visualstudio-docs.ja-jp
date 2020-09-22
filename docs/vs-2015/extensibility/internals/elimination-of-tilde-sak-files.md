---
title: ~ SAK Files | の削除Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 751acf4e5f56b7b477f05ab71571e0becd566649
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841508"
---
# <a name="elimination-of-sak-files"></a>~SAK ファイルの削除
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理プラグイン API 1.2 では、~ SAK ファイルは機能フラグと、ソース管理プラグインが MSSCCPRJ.SCC ファイルと共有チェックアウトをサポートしているかどうかを検出する新しい関数に置き換えられています。  
  
## <a name="sak-files"></a>~ SAK ファイル  
 Visual Studio .NET 2003 では、~ SAK で始まる一時ファイルが作成されました。 これらのファイルは、ソース管理プラグインが以下をサポートしているかどうかを判断するために使用されます。  
  
- MSSCCPRJ.SCC。SCC ファイル。  
  
- 複数の (共有) チェックアウト。  
  
  ソース管理プラグイン API 1.2 で提供される高度な機能をサポートするプラグインの場合、IDE は、次のセクションで詳しく説明する新しい機能、フラグ、および関数を使用して、一時ファイルを作成せずにこれらの機能を検出できます。  
  
## <a name="new-capability-flags"></a>新しい機能フラグ  
 `SCC_CAP_SCCFILE`  
  
 `SCC_CAP_MULTICHECKOUT`  
  
## <a name="new-functions"></a>新しい関数  
 [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)  
  
 [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)  
  
 ソース管理プラグインが複数の (共有) チェックアウトをサポートしている場合は、 `SCC_CAP_MULTICHECKOUT` 機能を宣言し、関数を実装し `SccIsMultiCheckOutEnabled` ます。 この関数は、ソース管理されたプロジェクトのいずれかでチェックアウト操作が行われるたびに呼び出されます。  
  
 ソース管理プラグインが、MSSCCPRJ.SCC の作成と使用をサポートしている場合。SCC ファイルでは、機能を宣言し、 `SCC_CAP_SCCFILE` [sccに](../../extensibility/sccwillcreatesccfile-function.md)よってファイルを実装します。 この関数は、ファイルの一覧を使用して呼び出されます。 関数は、 `TRUE/FALSE` Visual Studio で mssccprj.scc を使用する必要があるかどうかを示すために、各ファイルに対してを返します。そのための SCC ファイル。 ソース管理プラグインがこれらの新機能と機能をサポートしないことを選択した場合、次のレジストリキーを使用してこれらのファイルの作成を無効にすることができます。  
  
 [HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateTemporaryFilesInSourceControl" = dword: 00000001  
  
> [!NOTE]
> このレジストリキーが dword: 00000000 に設定されている場合は、キーが存在しないことに相当し、Visual Studio は一時ファイルの作成を試みます。 ただし、レジストリキーが dword: 00000001 に設定されている場合、Visual Studio は一時ファイルを作成しません。 代わりに、ソース管理プラグインが MSSCCPRJ.SCC をサポートしていないことを前提としています。SCC ファイルで、共有チェックアウトはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
