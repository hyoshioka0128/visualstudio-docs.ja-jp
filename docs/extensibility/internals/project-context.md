---
title: プロジェクトコンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: d1803f4a-24eb-44b0-b5d2-cb40c15534be
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 51e411f0bca361f96cdffcfd89498908fd21d441
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706596"
---
# <a name="project-context"></a>プロジェクトのコンテキスト
ユーザーがプロジェクトやプロジェクト項目を追加または操作する場合、IDE はプロジェクトコンテキストの概念を使用して、さまざまな操作の実行方法を決定します。

 通常、ファイルは、ユーザーが **[新しいプロジェクト**] コマンドを選択して明示的に作成する標準プロジェクト オブジェクト**Open Project**です。 **File** このような場合、ファイルはプロジェクトのコンテキストで作成されて開かれ、プロジェクトタイプによってドキュメントを編集するためのコンテキストが定義されます。

 一部のプロジェクトは、非常に豊富なコンテキストを提供します。 たとえば、プロジェクトは、プロジェクト スコープ、プログラムによる名前空間、またはプロジェクト スコープのデータベース接続を管理してデータ バインディングを行います。 ユーザーは、ソリューション エクスプローラーに表示されるプロジェクト項目など、特定のプロジェクト オブジェクトを使用して、ファイルやデータベース接続を直接開くことができます。

 それ以外の場合、項目のプロジェクト コンテキストは明示的に指定されていません。 たとえば、ユーザーがファイルを開いて [**ファイル**] メニューの [**既存のファイルを開く**] をクリックした場合、デバッガーがファイルを操作するとき、またはユーザーが [**検索と置換**] ダイアログ ボックスの **[ファイル内を検索**] コマンドをクリックすると、アイテムのコンテキストは使用できません。 このような状況に対処するために、IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>はドキュメントを開く最適なプロジェクトを見つけるプロセスを管理するために呼び出します。

## <a name="see-also"></a>関連項目
- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
