---
title: カスタム ユーザー インターフェイス (ソース管理 VSPackage) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interface, source control packages
- source control packages, user interface
ms.assetid: f35ddb24-53bf-461e-b34f-7414f657c082
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6ef807cef17a6ca3cddfee05ba57ace27e34a9e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708930"
---
# <a name="custom-user-interface-source-control-vspackage"></a>カスタム ユーザー インターフェイス (ソース管理 VSPackage)
VSPackage は、Visual Studio コマンド テーブル (*.vsct*) ファイルを使用して、メニュー項目とその既定の状態を宣言します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) は、VSPackage が読み込まれるまで、既定の状態のメニュー項目を表示します。 その後、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>このメソッドが呼び出され、メニュー項目を有効または無効にします。

 VSPackage は、コマンド ユーザー インターフェイス (UI) コンテキストに応じて VSPackage を自動的に読み込むことができるようにレジストリ キーを設定できますが、通常、ソース管理の VSPackage は、特定の UI コンテキストに切り替えるだけでなく、要求に応じて読み込む必要があります。 **レジストリ**キーの詳細については、「 [VSPackages](../../extensibility/managing-vspackages.md)の管理 」を参照してください。

## <a name="vspackage-ui"></a>VS パッケージの UI
 ソース管理パッケージは VSPackage として実装され、 の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI は使用されません。 各ソース管理 VSPackage は、メニュー項目、メニュー グループ、ツール ウィンドウ、ツール バー、およびソース管理 VSPackage に固有のオプションを設定するために必要な UI などの独自の UI 要素を指定する必要があります。 これらの UI 要素は、静的または動的に有効にすることができます。 静的 UI 要素は *.vsct*ファイルで定義され、VSPackage が読み込まれているかどうかにかかわらず表示されます。 動的 UI 要素は、 などの<xref:EnvDTE.Constants.vsContextNoSolution>特定のコマンド UI コンテキストに応じて表示されるか、メソッドの呼び<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>出しの結果として表示される場合があります。 動的 UI 要素の可視性は、VSPackages の遅延読み込みの戦略に準拠しています。

## <a name="ui-constraints-on-source-control-vspackages"></a>ソース管理 VS パッケージに対する UI 制約
 ソース管理の VSPackage は、読み込まれた後、IDE から削除できないため、VSPackage は非アクティブ状態に入ることができる必要があります。 VSPackage がアクティブでなくなったという通知を受信すると、VSPackage はその UI を無効にし、外部の IDE 操作を無視します。 VSPackage がアクティブでない場合、VSPackage の<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>メソッドの実装は、コマンドを非表示にする必要があります。

 すべてのソース管理 VSPackage は`IVsSccProvider`、インターフェイスを実装する必要があります。 インターフェイス上の 2<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A>つの<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>メソッドと、VSPackage によって実装する必要があります。

 ソース管理の VSPackage は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>など<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>によって実装されるさまざまな IDE イベントをサブスクライブしている可能性があります。 また、VSPackage はレジストリ対応のコールバック インターフェイスを実装している<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>場合もあります。 これらのインターフェイスは、非アクティブの場合は無視する必要があります。

 ソース管理の VSPackage のアクティブな状態の影響を受けるインターフェイスを次の一覧に示します。

- プロジェクト ドキュメントイベントを追跡します。

- ソリューション イベント。

- ソリューション永続性インターフェイス。 非アクティブの場合、パッケージは *.sln*ファイルと *.suo*ファイルに書き込まないようにします。

- プロパティ エクステンダー。

  ソース管理<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>VSPackage が非アクティブの場合、ソース管理に関連付けられている必須および 、および 、およびすべての省略可能なインターフェイスは呼び出されません。

  IDE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]が起動すると[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、コマンド UI コンテキストに現在の既定のソース管理 VSPackage ID の ID が設定されます。 これにより、アクティブなソース管理の VSPackage の静的 UI が実際に読み込まずに、IDE に表示されます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、VSPackage を呼び出[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]す前<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>に、 を通じて登録する VSPackage を一時停止します。

  次の表では、IDE がさまざまな[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 項目を非表示にする方法について詳しく説明します。

| UI 項目 | 説明 |
| - | - |
| メニューとツールバー | ソース管理パッケージは *、.vsct*ファイルの[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)セクションで、ソース管理パッケージ ID に初期メニューとツール バーの表示状態を設定する必要があります。 これにより、VSPackage を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]読み込み、メソッドの実装を呼び出すことなく、メニュー項目の状態を<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>適切に設定できます。 |
| ツール ウィンドウ | ソース 管理の VSPackage は、非アクティブになったときに、所有しているツール ウィンドウを非表示にします。 |
| ソース管理 VS パッケージ固有のオプション ページ | レジストリ キー **HKLM\ソフトウェア\マイクロソフト\VisualStudio\X\Y\ツールオプションページ\可視性CmdUIコンテキスト**を使用すると、VSPackage はオプション ページを表示する必要があるコンテキストを設定できます。 このキーの下のレジストリ エントリは、ソース管理サービスのサービス ID (SID) を使用して作成し、DWORD 値 1 を割り当てることによって作成する必要があります。 ソース管理の VSPackage が登録されているコンテキストで UI イベントが発生するたびに、VSPackage がアクティブな場合は、呼び出されます。 |

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterScciProvider>
- <xref:EnvDTE.Constants.vsContextNoSolution>
- [VSPackage を管理する](../../extensibility/managing-vspackages.md)
