---
title: その他のファイル プロジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 95cc1312fb7b381e1e20df834698480295fadcc8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707095"
---
# <a name="miscellaneous-files-project"></a>その他のファイル プロジェクト
ユーザーがプロジェクト項目を開くと、IDE は、ソリューション内のプロジェクトのメンバーではない項目をその他のファイル プロジェクトに割り当てます。

 プロジェクトは、ユーザーがプロジェクト項目を開くときにどのエディターを使用するかを決定する上で重要な役割を果たします。 プロジェクトは、プロジェクト固有のエディターまたは標準エディターを使用して、特定のファイルを開くように設計できます。

 プロジェクト固有のエディターでは、通常、ユーザーが特別な知識を持っているか、プロジェクトの特別なインターフェイスを使用する必要があります。 詳細については、「[方法 : プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)」を参照してください。

 標準エディターは、任意のプロジェクトで特定の拡張子の任意のファイルを開くことができます。 ユーザーは、テキスト エディタなどの一部の標準エディタ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をプロジェクト用にカスタマイズできますが、公開文字はそのまま保持できます。 標準エディターは、 メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>使用して作成されます。

 ソリューション内のプロジェクトがプロジェクト項目を開くことができると応答しない場合、IDE は、任意のファイルを開くその他のファイル プロジェクトと呼ばれる特別なプロジェクトを提供します。

 この特別なプロジェクトは、プロジェクトのコンテキスト外でファイルを開く場合に使用します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A>メソッドの処理中、その他のファイル プロジェクトは常に非常に低い優先順位で応答します。 したがって、その他のファイル プロジェクトは、ファイルを開くことができる優先度の高いプロジェクトを常に生成します。

 その他のファイル プロジェクトでは、ユーザーが **[新しいプロジェクト**] ダイアログ ボックスを使用して明示的に作成する必要はありません。 また、その他のファイル プロジェクトでは、プロジェクト メンバーの一覧を永続的に管理することはできません。 オプション機能を使用して、各ユーザーの最近使用したファイルのリストを記録します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)
- [方法: 標準のエディターを開く](../../extensibility/how-to-open-standard-editors.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [プロジェクト テンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)
