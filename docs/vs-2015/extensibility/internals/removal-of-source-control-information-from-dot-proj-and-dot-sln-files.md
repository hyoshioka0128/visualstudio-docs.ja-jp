---
title: からソース管理情報を削除しています。Proj と。.Sln ファイル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b7cdaeb02f77d3775096f840a513f68e531b1299
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199376"
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>.Proj および .Sln ファイルからのソース管理情報の削除
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理プラグイン API のバージョン1.2 では、SCC 情報は MSSCCPRJ.SCC に格納されます。SCC ファイル。 MSSCCPRJ.SCC の利点。SCC ファイルとは、SCC 情報がソース管理されていないということです。これは、tfsbuild.proj ファイルや .sln ファイルなどにあります。  
  
## <a name="version-12-changes"></a>バージョン1.2 の変更  
 ソース管理プラグイン API バージョン1.1 に基づくソース管理プラグインでは、ソース管理に関する情報がプロジェクト (proj) ファイルとソリューション (.sln) ファイルに格納されます。 ソース管理情報のデータベースの場所は、「データソース」によって指定され、データベース内の特定の場所は ProjName によって指定されます。 この動作により、分岐、フォーク、またはコピー操作後に問題が発生する可能性があります。これは、これらの操作のいずれかを実行した後、ProjName が通常は無効になるためです。  
  
 ソース管理プラグイン API バージョン1.1 では、IDE では、プラグインが MSSCCPRJ.SCC をサポートしているかどうかを検出するために、~ SAK ファイルが使用されていました。ソース管理情報を格納する SCC メソッド。 ソース管理プラグイン API バージョン1.2 には、MSSCCPRJ.SCC のサポートを検出するための新しい機能が用意されています。~ SAK ファイルを使用しない SCC ファイル。 詳細については、「 [~ SAK ファイルの削除](../../extensibility/internals/elimination-of-tilde-sak-files.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
