---
title: プロジェクトの優先度 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a75c1c333d88e1bf5524281bee8b2a683ca6c98e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706420"
---
# <a name="project-priority"></a>プロジェクトの優先順位
プロジェクト項目は通常、ソリューション内の 1 つのプロジェクトのみのメンバーです。 そのため、IDE は、アイテムを開くために使用するプロジェクトを簡単に判断できます。 ただし、項目が複数のプロジェクトのメンバーである場合、IDE は優先度スキームを使用して、項目を開くための最適なプロジェクトを決定します。

 次の一覧は、プロジェクトの優先順位のスキームを示しています。

- IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A>ソリューション内の各プロジェクトのメソッドを呼び出して、ドキュメントがそのプロジェクトのメンバーであるかどうかを判断します。

- ドキュメントがプロジェクトのメンバーである場合、プロジェクトは、そのドキュメントの処理に従ってプロジェクトが割り当てる優先度で応答します。 たとえば、言語プロジェクトは言語ソースファイルの優先度が高い応答を返しますが、ビルドプロセスの一部として使用されていない認識されないファイルの種類に対して低い優先順位で応答します。

- ドキュメントに対してプロジェクト固有のカスタム エディターやデザイナーを提供するプロジェクトも、優先度が高くなります。

- 列挙<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>体は、ドキュメントの優先順位の値を提供します。

- 最も優先度の高いプロジェクトには、ドキュメントを開くコンテキストが与えられます。 2 つのプロジェクトが同じ優先度の値を返す場合は、アクティブなプロジェクトが優先されます。 ソリューション内のプロジェクトがドキュメントを開くことができると応答しない場合、IDE はそのドキュメントをその他のファイル プロジェクトに配置します。 詳細については、「[その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)
- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
