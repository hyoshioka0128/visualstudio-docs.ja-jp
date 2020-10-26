---
title: プロジェクトの優先順位 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706420"
---
# <a name="project-priority"></a>プロジェクトの優先順位
通常、プロジェクトアイテムは、ソリューション内の1つのプロジェクトのメンバーです。 そのため、IDE では、項目を開くために使用されるプロジェクトを簡単に判断できます。 ただし、1つの項目が複数のプロジェクトのメンバーである場合、IDE は優先度スキームを使用して、項目を開くのに最適なプロジェクトを決定します。

 次の一覧は、プロジェクトの優先度スキームを示しています。

- IDE は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> ソリューション内のプロジェクトごとにメソッドを呼び出して、ドキュメントがそのプロジェクトのメンバーであるかどうかを確認します。

- ドキュメントがプロジェクトのメンバーである場合、プロジェクトは、そのドキュメントの処理に従ってプロジェクトが割り当てた優先度で応答します。 たとえば、言語プロジェクトは、言語ソースファイルに対して高い優先度で応答しますが、ビルドプロセスの一部として使用されていない、認識されないファイルの種類に対しては低い優先順位で応答します。

- ドキュメントに対して、プロジェクト固有のカスタムエディターまたはデザイナーを提供するプロジェクトも、優先度が高くなります。

- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>列挙体は、ドキュメントの優先順位の値を提供します。

- 最も高い優先順位を指定するプロジェクトには、ドキュメントを開くコンテキストが付与されます。 2つのプロジェクトが同じ優先順位値を返す場合、アクティブなプロジェクトが優先されます。 ソリューション内のプロジェクトがドキュメントを開くことができない場合、IDE はそのドキュメントを [その他のファイル] プロジェクトに配置します。 詳細については、「 [その他のファイルプロジェクト](../../extensibility/internals/miscellaneous-files-project.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)
- [方法: 開いているドキュメントのエディターを開く](../../extensibility/how-to-open-editors-for-open-documents.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
