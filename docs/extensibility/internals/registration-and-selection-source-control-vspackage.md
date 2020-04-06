---
title: 登録と選択 (ソース管理 VS パッケージ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 973eb19916a737dfa775fe79ee62cb3d11fe0123
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705720"
---
# <a name="registration-and-selection-source-control-vspackage"></a>登録と選択 (ソース管理 VSPackage)
ソース管理の VSPackage をに公開するには、VSPackage を登録する必要があります[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 複数のソース管理 VSPackage が登録されている場合、ユーザーは適切な時間に読み込む VSPackage を選択できます。 [VS パッケージ](../../extensibility/internals/vspackages.md)の詳細と、それらを登録する方法については、VSPackages を参照してください。

## <a name="registering-a-source-control-package"></a>ソース管理パッケージの登録
 ソース管理パッケージは、環境がサポートされている[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]機能を検索してクエリできるように登録されます。 これは、パッケージのインスタンスが、その機能またはコマンドが必要な場合、または明示的に要求された場合にのみ作成される遅延読み込みスキームに従って行われます。

 VSPackages は、バージョン固有のレジストリ キーHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y*に情報を*格納します。* *Y* この実習では、 の複数のバージョンのサイド バイ サイド インストール[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をサポートする機能を提供します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザー インターフェイス (UI) は、複数のインストールされているソース管理プラグイン (ソース管理アダプター パッケージ経由) とソース管理 VSPackages の中から選択をサポートします。 アクティブなソース管理プラグインまたは VSPackage は一度に 1 つのみ存在できます。 ただし、後述のように、IDE では、自動ソリューション ベースのパッケージスワッピングメカニズムを使用してソース管理プラグインと VSPackage を切り替えます。 ソース管理 VSPackage の一部には、この選択メカニズムを有効にするいくつかの要件があります。

### <a name="registry-entries"></a>レジストリ エントリ
 ソース管理パッケージには、次の 3 つのプライベート GUID が必要です。

- パッケージ GUID: これは、ソース管理の実装 (このセクションでID_Package呼ばれます) を含むパッケージのメイン GUID です。

- ソース管理 GUID: これは、Visual Studio ソース管理スタブに登録するために使用されるソース管理 VSPackage の GUID であり、コマンド UI コンテキスト GUID としても使用されます。 ソース管理サービスの GUID は、ソース管理の GUID で登録されます。 この例では、ソース管理の GUID はID_SccProvider呼び出されます。

- ソース管理サービス GUID: これは Visual Studio で使用されるプライベート サービス GUID です (このセクションではSID_SccPkgService呼ばれます)。 これに加えて、ソース管理パッケージは VSPackage、ツール ウィンドウなどの他の GUID を定義する必要があります。

  ソース管理 VSPackage によって次のレジストリ エントリを作成する必要があります。

| キー名 | エントリ |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (デフォルト) = rg_sz:{ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | (デフォルト) =\<rg_sz: パッケージ>のフレンドリ名<br /><br /> サービス = rg_sz:{SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | (既定) = rg_sz:#\<ローカライズされた名前のリソース ID><br /><br /> パッケージ = rg_sz:{ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (キー名は、既に`SourceCodeControl`使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]されており、PackageName>の選択肢としては使用できないこと\<に注意してください。 | (デフォルト) = rg_sz:{ID_Package} |

## <a name="selecting-a-source-control-package"></a>ソース管理パッケージの選択
 複数のソース管理プラグイン API ベースのプラグインとソース管理 VSPackage を同時に登録できます。 ソース管理プラグインまたは VSPackage を選択するプロセスは、プラグインまたは[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage を適切なタイミングで読み込み、必要になるまで不要なコンポーネントの読み込みを延期できるようにする必要があります。 さらに、メニュー[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]項目、ダイアログ ボックス、およびツール バーを含む他の非アクティブな VSPackage からすべての UI を削除し、アクティブな VSPackage の UI を表示する必要があります。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]次のいずれかの操作が実行されると、ソース管理の VSPackage が読み込まれます。

- ソリューションが開かれます (ソリューションがソース管理下にある場合)。

   ソース管理下のソリューションまたはプロジェクトを開くと、IDE によって、そのソリューション用に指定されたソース管理 VSPackage が読み込まれます。

- ソース管理 VSPackage のメニュー コマンドのいずれかが実行されます。

  ソース管理 VSPackage は、必要なコンポーネントを実際に使用する場合にのみ読み込む必要があります (遅延読み込みとも呼ばれます)。

### <a name="automatic-solution-based-vspackage-swapping"></a>ソリューション ベースの VS パッケージの自動スワップ
 ソース管理 VSPackages は、ソース管理[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**カテゴリの**[**オプション]** ダイアログ ボックスで手動で交換できます。 ソリューション ベースのパッケージの自動スワップは、特定のソリューションに対して指定されているソース管理パッケージが、そのソリューションを開いたときに自動的にアクティブに設定されることを意味します。 すべてのソース管理パッケージは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A>と を実装する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理プラグイン (ソース管理プラグイン API の実装) とソース管理 VSPackages の両方の間の切り替えを処理します。

 ソース管理アダプター パッケージは、ソース管理プラグイン API ベースのプラグインに切り替えるために使用されます。 中間ソース管理アダプター パッケージに切り替え、アクティブまたは非アクティブに設定する必要があるソース管理プラグインを決定するプロセスは、ユーザーに対して透過的です。 ソース管理プラグインがアクティブな場合、アダプタ パッケージは常にアクティブです。 2 つのソース管理プラグイン間の切り替えは、プラグイン DLL の読み込みとアンロードに相当します。 ただし、ソース管理 VSPackage への切り替えには、IDE と対話して適切な VSPackage を読み込む必要があります。

 ソース管理の VSPackage は、ソリューションが開かれ、VSPackage のレジストリ キーがソリューション ファイルにあるときに呼び出されます。 ソリューションを開くと、レジストリ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]値を検索し、適切なソース管理 VSPackage を読み込みます。 すべてのソース管理 VSPackages には、上記のレジストリ エントリが必要です。 ソース管理下にあるソリューションは、特定のソース管理 VSPackage に関連付けられているものとしてマークされます。 ソース管理 VSPackage は<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>、ソリューション ベースの VSPackage の自動スワップを有効にするを実装する必要があります。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>パッケージの選択と切り替えのための Visual Studio UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ソース管理の VSPackage とプラグインの選択の UI をソース**管理**カテゴリの下の **[オプション**] ダイアログ ボックスで提供します。 このオプションを使用すると、ユーザーはアクティブなソース管理プラグインまたは VSPackage を選択できます。 ドロップダウン リストには、次の項目が含まれます。

- インストールされているすべてのソース管理パッケージ

- インストールされているすべてのソース管理プラグイン

- ソース コード管理を無効にする "none" オプション

  アクティブなソース管理の選択項目の UI のみが表示されます。 VSPackage の選択は、以前の VSPackage の UI を非表示にし、新しい 1 つの UI を表示します。 アクティブな VSPackage は、ユーザーごとに選択されます。 ユーザーが同時に開いている複数[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のコピーを持っている場合、各ユーザーは、別のアクティブな VSPackage を使用する可能性があります。 複数のユーザーが同じコンピューターにログオンしている場合、各ユーザーは、それぞれ異なる[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]アクティブな VSPackage を持つ、開いているの別々のインスタンスを持つことができます。 ユーザーが複数のインスタンス[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を閉じると、最後に開いたソリューションでアクティブだったソース管理 VSPackage が既定のソース管理 VSPackage になり、再起動時にアクティブに設定されます。

  以前のバージョンと[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は異なり、IDE の再起動は、ソース管理 VSPackages を切り替える唯一の方法ではありません。 VS パッケージの選択は自動的に行われます。 パッケージの切り替えには、Windows ユーザー特権が必要です (管理者またはパワーユーザーではありません)。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [機能](../../extensibility/internals/source-control-vspackage-features.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
