---
title: 永続化と実行中のドキュメントテーブル |Microsoft Docs
description: プロジェクトが、Visual Studio IDE でドキュメントの状態を追跡する、実行中のドキュメントテーブルでのドキュメントのオープン、保存、および名前変更をコーディネートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, managing
- IVsPersistHierarchyItem interface, implementing
- architecture, persistence
- running document table (RDT), architecture
ms.assetid: 27117eae-6c58-4189-a61a-1397a43b5ecf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5244e14498da0f556a71b8d710ccbaa8b9b03e65
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095122"
---
# <a name="persistence-and-the-running-document-table"></a>ドキュメント テーブルの保存と実行
IDE で [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、プロジェクトは、サービスを使用して実行するプロジェクト項目の永続化を完全に管理し <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> ます。 ドキュメントは、Visual Studio 環境における永続化の基本単位です。 プロジェクトは、開いているすべてのドキュメントの状態を追跡するリソースである、実行中のドキュメントテーブル (RDT) を使用して、ドキュメントのオープン、保存、および名前変更を調整します。

## <a name="managing-persistence"></a>永続化の管理
 プロジェクトは、インターフェイスを実装することによって、環境の永続性サービスを制御し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> ます。 環境はドキュメントを直接保存するように要求することはありませんが、所有するプロジェクト (または階層) にドキュメントを保存するように要求します。 これにより、プロジェクトは、プロジェクトアイテムデータをローカルファイル、リモートファイル、データベース、リポジトリ、またはその他のメディアに保存することができます。

 グローバル環境では、RDT が維持されます。 この環境では、RDT 内の開いているすべてのウィンドウとドキュメントのエントリを保持します。これにより、ソリューションが閉じられたときなど、特別な通知を受け取ることができます。 さらに、RDT を使用すると、環境が **ソリューションエクスプローラー** 内の対応するノードを追跡できるようになります。 RDT は、プロジェクトファイルとプロジェクト項目ドキュメントの両方を含めて、開いている持続可能なオブジェクトごとに1つのレコードを保持します。

## <a name="see-also"></a>こちらもご覧ください
- [ドキュメント テーブルの実行](../../extensibility/internals/running-document-table.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
