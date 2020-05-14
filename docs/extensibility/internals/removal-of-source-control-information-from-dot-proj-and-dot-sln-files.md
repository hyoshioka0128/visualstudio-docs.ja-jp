---
title: .proj ファイルおよび .sln ファイルからソース管理情報を削除する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba3085a7806bfb0556613d1fca1b94953dcdb0b2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705582"
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>.Proj および .Sln ファイルからのソース管理情報の削除
ソース管理プラグイン API のバージョン 1.2 では、SCC 情報は MSSCCPRJ に格納されます。SCC ファイル。 MSSCCPRJの利点。SCC ファイルは、SCC 情報がソース管理されていないということです。

## <a name="version-12-changes"></a>バージョン 1.2 の変更点
 ソース管理プラグイン API バージョン 1.1 に基づくソース管理プラグインでは、ソース管理に関する情報はプロジェクト (.proj) およびソリューション (.sln) ファイルに格納されます。 ソース管理情報のデータベースの場所は AuxPath によって指定され、データベース内の特定の場所は ProjName で指定されます。 この動作は、これらの操作の後に ProjName が通常無効になるため、分岐、分岐、またはコピー操作の後に問題が発生する可能性があります。

 ソース管理プラグイン API バージョン 1.1 では、IDE は 、プラグインが MSSCCPRJ をサポートしているかどうかを検出するために ~SAK ファイルを使用しました。ソース管理情報を格納する SCC メソッド。 ソース管理プラグイン API バージョン 1.2 は、MSSCCPRJ のサポートを検出するための新しい機能を提供します。SAK ファイルを使用しない SCC ファイル。 詳細については、「 [~SAK ファイルの削除](../../extensibility/internals/elimination-of-tilde-sak-files.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
