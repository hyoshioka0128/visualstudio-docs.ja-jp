---
title: プロジェクト項目を開いて保存する |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706966"
---
# <a name="opening-and-saving-project-items"></a>プロジェクト項目のオープンと保存
新しいプロジェクトの種類を追加する場合は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) でのプロジェクトファイルのオープンと保存を管理する必要があります。 次のトピックでは、ファイルを開いたり保存したりするためのさまざまな方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [ファイルを開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-file-command.md)

 IDE で [ **ファイルを開く** ] コマンドを処理する方法と、このコマンドに応答するプロジェクトのロールについて、順を追って説明します。

- [プログラムから開くコマンドを使用したファイルの表示](../../extensibility/internals/displaying-files-by-using-the-open-with-command.md)

 IDE で **Open With** コマンドがどのように処理されるかについて、詳細な手順について説明します。これにより、標準エディターを選択したファイルを開くように求められます。

- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクト固有のエディターを使用して、プロジェクト内の特定の種類のファイルを開く必要があることを指定する手順について説明します。

- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)

 IDE でプロジェクトの種類のファイルの標準エディターを開く方法を指定する手順について説明します。

- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)

 開いているファイルのプロジェクト固有のエディターを開く手順について説明します。

- [標準ドキュメントの保存](../../extensibility/internals/saving-a-standard-document.md)

 標準エディターで開かれたドキュメントに対して、[ **保存**]、[名前を付け **て保存**]、および [ **すべて** を保存] コマンドを IDE で処理する方法について詳しく説明します。

- [カスタム ドキュメントの保存](../../extensibility/internals/saving-a-custom-document.md)

 カスタムエディターで開かれたドキュメントに対して、[ **保存**]、[名前を付け **て保存**]、[すべてを保存]、および [ **すべて** を保存] の各コマンドを IDE で処理する方法について、図と詳細な説明

- [プロジェクトでのファイルを開くエディターの決定](../../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)

 ファイルに適切なエディターまたはデザイナーを選択するために IDE が従うプロセスについて説明します。

## <a name="related-sections"></a>関連項目
- [カスタム エディターとデザイナーの作成](../../extensibility/creating-custom-editors-and-designers.md)

 IDE がホストできる4種類のエディターを一覧表示し、各エディターの説明を示します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 プロジェクトが、コードのコンパイルとビルドの方法、エディターのオープン方法、およびプロジェクト項目の書式設定方法について説明します。
