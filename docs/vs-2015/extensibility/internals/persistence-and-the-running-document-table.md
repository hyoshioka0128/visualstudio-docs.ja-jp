---
title: 永続化と実行中のドキュメントテーブル |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2c422ad1735312c82c8dc027c4adf73c1b033685
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196085"
---
# <a name="persistence-and-the-running-document-table"></a>ドキュメント テーブルの保存と実行
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

IDE で [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、プロジェクトは、サービスを使用して実行するプロジェクト項目の永続化を完全に管理し <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> ます。 ドキュメントは、Visual Studio 環境における永続化の基本単位です。 プロジェクトは、開いているすべてのドキュメントの状態を追跡するリソースである、実行中のドキュメントテーブル (RDT) を使用して、ドキュメントのオープン、保存、および名前変更を調整します。  
  
## <a name="managing-persistence"></a>永続化の管理  
 プロジェクトは、インターフェイスを実装することによって、環境の永続性サービスを制御し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> ます。 環境はドキュメントを直接保存するように要求することはありませんが、所有するプロジェクト (または階層) にドキュメントを保存するように要求します。 これにより、プロジェクトは、プロジェクトアイテムデータをローカルファイル、リモートファイル、データベース、リポジトリ、またはその他のメディアに保存することができます。  
  
 グローバル環境では、RDT が維持されます。 この環境では、RDT 内の開いているすべてのウィンドウとドキュメントのエントリを保持します。これにより、ソリューションが閉じられたときなど、特別な通知を受け取ることができます。 さらに、RDT を使用すると、環境が **ソリューションエクスプローラー**内の対応するノードを追跡できるようになります。 RDT は、プロジェクトファイルとプロジェクト項目ドキュメントの両方を含めて、開いている持続可能なオブジェクトごとに1つのレコードを保持します。  
  
## <a name="see-also"></a>参照  
 [実行 (ドキュメントテーブルを)](../../extensibility/internals/running-document-table.md)   
 [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
