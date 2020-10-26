---
title: プロジェクトコンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d4ee4da5fdea63cf1bdd33554c72f6dac30d0334
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62429939"
---
# <a name="project-context"></a>プロジェクトのコンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ユーザーがプロジェクトおよびプロジェクト項目を追加または操作すると、IDE はプロジェクトコンテキストの概念を使用して、さまざまな操作を実行する方法を決定します。  
  
 通常、ファイルは、ユーザーが [**新しいプロジェクト**] コマンドを選択して明示的に作成するか、[**ファイル**] メニューの [**プロジェクトを開く**] コマンドを選択して使用できるようにすることで、ユーザーが明示的に作成する標準のプロジェクトオブジェクトです。 このような場合は、ファイルが作成され、プロジェクトのコンテキストで開かれます。また、プロジェクトの種類は、ドキュメントを編集するためのコンテキストを定義します。  
  
 一部のプロジェクトは、非常に豊富なコンテキストを提供します。 たとえば、プロジェクトでは、プロジェクトスコープのプログラムによる名前空間またはデータバインディングのためのプロジェクトスコープデータベース接続を管理します。 ユーザーは、ソリューションエクスプローラーに表示されるプロジェクト項目などの特定のプロジェクトオブジェクトを使用して、ファイルまたはデータベース接続を直接開くことができます。  
  
 それ以外の場合は、項目のプロジェクトコンテキストが明示的に指定されていません。 たとえば、ユーザーがファイルを開いたときに、[**ファイル**] メニューの [**既存のファイルを開く**] コマンドを選択するか、デバッガーがファイルを操作するとき、または [**検索と置換**] ダイアログボックスでユーザーが [**フォルダーを**選択して検索] コマンドをクリックしたときに、項目のコンテキストを使用することはできません。 このような状況に対処するために、IDE はを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> ドキュメントを開くための最適なプロジェクトの検索プロセスを管理します。  
  
## <a name="see-also"></a>参照  
 [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)   
 [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
