---
title: プロジェクト内のファイルを開くエディタを決定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], determining which editor opens a file
- projects [Visual Studio SDK], determining which editor opens file
- project types, determining which editor opens a file
- persistence, determining which editor opens a file
ms.assetid: acbcf4d8-a53a-4727-9043-696a47369479
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af7037a3b4bfbae1801e802256af240d017d2789
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708656"
---
# <a name="determine-which-editor-opens-a-file-in-a-project"></a>プロジェクト内のファイルを開くエディタを決定する
ユーザーがプロジェクト内のファイルを開くと、環境はポーリング プロセスを経て、最終的にそのファイルに適したエディターまたはデザイナーを開きます。 環境で使用される最初の手順は、標準エディターとカスタム エディターの両方で同じです。 環境では、ファイルを開くために使用するエディターをポーリングするときにさまざまな条件を使用し、VSPackage はこのプロセス中に環境と調整する必要があります。

 たとえば、ユーザーが **[ファイル]** メニューの **[開く**] をクリックし *、filename.rtf* (または*拡張子が .rtf*のファイル) を<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>選択すると、環境は各プロジェクトの実装を呼び出し、最終的にソリューション内のすべてのプロジェクト インスタンスを循環させます。 プロジェクトは、優先度によってドキュメントの要求を識別するフラグのセットを返します。 最も高い優先順位を使用して、環境<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>は適切なメソッドを呼び出します。 ポーリングプロセスの詳細については、「[プロジェクトテンプレートとプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

 その他のファイル プロジェクトでは、他のプロジェクトによって要求されていないすべてのファイルが要求されます。 これにより、カスタム エディターは、標準のエディターを開く前にドキュメントを開くことができます。 その他のファイル プロジェクトがファイルを要求する場合、環境は、標準<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>エディターでファイルを開くメソッドを呼び出します。 この環境では、登録されているエディターの内部リストで *、.rtf*ファイルを処理するエディターがチェックされます。 この一覧は、次のキーのレジストリにあります。

 **HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\VisualStudio\\\<バージョン>\\\\<エディター エディター ファクトリ ガイド>\拡張機能**

 また、サブキー **DocObject**を持つオブジェクトの**HKEY_CLASSES_ROOT\CLSID**キーのクラス識別子もチェックされます。 ファイル拡張子が見つかった場合は、埋め込まれたバージョンの Microsoft Word などのアプリケーションが、Visual Studio で埋め込み先で作成されます。 これらのドキュメント オブジェクトは、インターフェイスを実装する<xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>複合ファイルである必要があります<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>。

 レジストリに *.rtf*ファイルのエディター ファクトリがない場合、環境は**HKEY_CLASSES_ROOT\\.rtf**キーを検索し、そこで指定されたエディターを開きます。 ファイル拡張子が**HKEY_CLASSES_ROOT**で見つからない場合、環境では Visual Studio のコア テキスト エディターを使用してファイルを開きます (テキスト ファイルの場合)。

 コア テキスト エディターが失敗した場合 (ファイルがテキスト ファイルでない場合に発生する)、環境では、そのファイルのバイナリ エディターが使用されます。

 環境は、そのレジストリ内の *.rtf*拡張機能のエディターを見つける場合は、このエディター ファクトリを実装する VSPackage を読み込みます。 環境は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>新しい VSPackage のメソッドを呼び出します。 VSPackage は`QueryService``SID_SVsRegistorEditor`、エディター ファクトリ<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A>を環境に登録するメソッドを使用して を呼び出します。

 この環境では、登録されているエディターの内部リストを再確認して、新たに登録された *.rtf*ファイル用のエディター ファクトリを見つけます。 環境は、作成する<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>ファイル名とビューの種類を渡して、メソッドの実装を呼び出します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>
- <xref:Microsoft.VisualStudio.OLE.Interop.IPersistStorage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>
