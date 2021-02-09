---
title: プロジェクトコンテキスト |Microsoft Docs
description: Visual Studio IDE でプロジェクトコンテキストを使用して、ユーザーがプロジェクトおよびプロジェクト項目を追加または操作するときに操作を実行する方法を決定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fdc5550cfde44c71b1b663a30cf1824c6edfcf82
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907679"
---
# <a name="project-context"></a>プロジェクトのコンテキスト
ユーザーがプロジェクトおよびプロジェクト項目を追加または操作すると、IDE はプロジェクトコンテキストの概念を使用して、さまざまな操作を実行する方法を決定します。

 通常、ファイルは、ユーザーが [**新しいプロジェクト**] コマンドを選択して明示的に作成するか、[**ファイル**] メニューの [**プロジェクトを開く**] コマンドを選択して使用できるようにすることで、ユーザーが明示的に作成する標準のプロジェクトオブジェクトです。 このような場合は、ファイルが作成され、プロジェクトのコンテキストで開かれます。また、プロジェクトの種類は、ドキュメントを編集するためのコンテキストを定義します。

 一部のプロジェクトは、非常に豊富なコンテキストを提供します。 たとえば、プロジェクトでは、プロジェクトスコープのプログラムによる名前空間またはデータバインディングのためのプロジェクトスコープデータベース接続を管理します。 ユーザーは、ソリューションエクスプローラーに表示されるプロジェクト項目などの特定のプロジェクトオブジェクトを使用して、ファイルまたはデータベース接続を直接開くことができます。

 それ以外の場合は、項目のプロジェクトコンテキストが明示的に指定されていません。 たとえば、ユーザーがファイルを開いたときに、[**ファイル**] メニューの [**既存のファイルを開く**] コマンドを選択するか、デバッガーがファイルを操作するとき、または [**検索と置換**] ダイアログボックスでユーザーが [**フォルダーを** 選択して検索] コマンドをクリックしたときに、項目のコンテキストを使用することはできません。 このような状況に対処するために、IDE はを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> ドキュメントを開くための最適なプロジェクトの検索プロセスを管理します。

## <a name="see-also"></a>関連項目
- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
