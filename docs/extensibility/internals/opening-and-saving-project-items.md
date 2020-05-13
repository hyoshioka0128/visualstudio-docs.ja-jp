---
title: プロジェクトアイテムを開いて保存する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], file persistence
- files [Visual Studio], opening and saving
- editors [Visual Studio SDK], file persistence
ms.assetid: f71898ad-335f-4c43-a177-4da87078afd1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbb89d99e401be6bae7d8ee9be8ee33fa7574723
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706966"
---
# <a name="opening-and-saving-project-items"></a>プロジェクト項目のオープンと保存
新しいプロジェクトタイプを追加する場合、統合開発環境 (IDE) でプロジェクトファイルの開[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]いて保存する作業を管理する必要があります。 次のトピックでは、ファイルを開いて保存するさまざまな方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [ファイルを開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 IDE が **[ファイルを開く]** コマンドを処理する方法と、このコマンドに応答するプロジェクトの役割について、手順を追って説明します。

- [プログラムから開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 IDE が [**プログラムから開く**] コマンドを処理する方法について、詳細な手順を説明し、標準エディターを選択したファイルを開く場合の確認を促します。

- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクト固有のエディターを使用して、プロジェクト内の特定の種類のファイルを開く必要があることを指定する手順について説明します。

- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)

 IDE でプロジェクトの種類のファイル用の標準エディターを開くようにする方法を指定する手順について説明します。

- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)

 開いているファイルのプロジェクト固有のエディターを開く手順について説明します。

- [標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)

 標準エディタで開いたドキュメントの **[保存]、[****名前を付けて保存**]、および [**すべて保存]** コマンドを IDE で処理する方法について詳しく説明します。

- [カスタム ドキュメントの保存](../../extensibility/internals/saving-a-custom-document.md)

 カスタム エディターで開いたドキュメントの **[保存]、[名前****を付けて保存**]、[**すべて保存]** の各コマンドを IDE で処理する方法を図と詳細に説明します。

- [プロジェクトでのファイルを開くエディターの決定](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 IDE がファイルに適したエディタまたはデザイナを選択するプロセスについて説明します。

## <a name="related-sections"></a>関連項目
- [カスタム エディターとデザイナーの作成](../../extensibility/creating-custom-editors-and-designers.md)

 IDE がホストできる 4 種類のエディタの一覧と、各エディターの説明を示します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 コードのコンパイル方法とビルド方法、エディターを開く方法、およびプロジェクト項目の書式設定方法をプロジェクトが制御する方法について説明します。
