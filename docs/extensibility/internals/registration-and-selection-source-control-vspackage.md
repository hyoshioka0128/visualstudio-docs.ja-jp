---
title: 登録と選択 (ソース管理 VSPackage) |Microsoft Docs
description: ソース管理 VSPackage を Visual Studio に登録する方法と、複数の登録済みソース管理パッケージから読み込むパッケージを選択する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 76f0bd737eff52706cf73c9a1105b79e08c556f0
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877365"
---
# <a name="registration-and-selection-source-control-vspackage"></a>登録と選択 (ソース管理 VSPackage)
に公開するには、ソース管理 VSPackage を登録する必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 複数のソース管理 VSPackage が登録されている場合、ユーザーは適切なタイミングで読み込む VSPackage を選択できます。 Vspackage とその登録方法の詳細については、「 [vspackage](../../extensibility/internals/vspackages.md) 」を参照してください。

## <a name="registering-a-source-control-package"></a>ソース管理パッケージの登録
 ソース管理パッケージが登録されているため、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境でサポートされている機能を検索してクエリを実行できます。 これは、機能またはコマンドが必要な場合、または明示的に要求された場合にのみ、パッケージのインスタンスが作成される遅延読み込みスキームに従っています。

 Vspackage はバージョン固有のレジストリキー (x \\ はメジャーバージョン番号、 *y* はマイナー バージョン番号) に情報 *を HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudioします。* この方法では、複数のバージョンののサイドバイサイドインストールをサポートでき [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ユーザーインターフェイス (UI) は、インストールされている複数のソース管理プラグイン (ソース管理アダプターパッケージを使用) からの選択、およびソース管理 vspackage をサポートします。 アクティブなソース管理プラグインまたは VSPackage は一度に1つしか存在できません。 ただし、以下で説明するように、IDE では、ソリューションベースの自動パッケージスワップメカニズムを使用して、ソース管理プラグインと Vspackage を切り替えることができます。 この選択メカニズムを有効にするために、ソース管理 VSPackage の一部にはいくつかの要件があります。

### <a name="registry-entries"></a>レジストリ エントリ
 ソース管理パッケージには、次の3つのプライベート Guid が必要です。

- パッケージ GUID: これは、ソース管理の実装 (このセクションで ID_Package と呼ばれます) を含むパッケージの主要な GUID です。

- ソース管理 GUID: これは、Visual Studio ソース管理スタブに登録するために使用されるソース管理 VSPackage の GUID であり、コマンド UI コンテキスト GUID としても使用されます。 ソース管理サービス GUID は、ソース管理 GUID の下に登録されます。 この例では、ソース管理 GUID は ID_SccProvider と呼ばれています。

- ソース管理サービス GUID: これは、Visual Studio によって使用されるプライベートサービス GUID です (このセクションで SID_SccPkgService と呼ばれます)。 さらに、ソース管理パッケージでは、Vspackage、ツールウィンドウなどの他の Guid を定義する必要があります。

  次のレジストリエントリは、ソース管理 VSPackage によって作成される必要があります。

| キー名 | エントリ |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (既定値) = rg_sz: {ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | (既定値) = rg_sz:\<Friendly name of Package><br /><br /> サービス = rg_sz: {SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | (既定値) = rg_sz:#\<Resource ID for localized name><br /><br /> パッケージ = rg_sz: {ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (キー名は、に `SourceCodeControl` よって既に使用されて [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] おり、の選択肢として使用できないことに注意して \<PackageName> ください)。 | (既定値) = rg_sz: {ID_Package} |

## <a name="selecting-a-source-control-package"></a>ソース管理パッケージの選択
 いくつかのソース管理プラグイン API ベースのプラグインとソース管理 Vspackage が同時に登録されている可能性があります。 ソース管理プラグインまたは VSPackage を選択するプロセスでは、がプラグインまたは VSPackage を適切なタイミングで読み込むことを確認する必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。また、必要になるまで不要なコンポーネントの読み込みを遅延させることができます。 さらに、は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] メニュー項目、ダイアログボックス、ツールバーなど、他の非アクティブな vspackage からすべての ui を削除し、アクティブな VSPackage の ui を表示する必要があります。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 次のいずれかの操作が実行されたときに、ソース管理 VSPackage を読み込みます。

- ソリューションが開かれています (ソリューションがソース管理下にある場合)。

   ソース管理下にあるソリューションまたはプロジェクトを開くと、IDE によって、そのソリューションに対して指定されたソース管理 VSPackage が読み込まれます。

- ソース管理 VSPackage のメニューコマンドが実行されます。

  ソース管理 VSPackage は、実際に使用される場合にのみ必要なコンポーネント (遅延読み込みとも呼ばれます) を読み込む必要があります。

### <a name="automatic-solution-based-vspackage-swapping"></a>ソリューションベースの VSPackage の自動スワップ
 ソース管理の Vspackage は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [ **オプション** ] ダイアログボックスの [ **ソース管理** ] カテゴリで手動で切り替えることができます。 ソリューションベースの自動パッケージスワップは、特定のソリューションに対して指定されているソース管理パッケージが、そのソリューションを開いたときに自動的にアクティブに設定されることを意味します。 すべてのソース管理パッケージは、とを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> ます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ソース管理プラグイン (ソース管理プラグイン API の実装) とソース管理 Vspackage の間の切り替えを処理します。

 ソース管理アダプターパッケージは、任意のソース管理プラグイン API ベースのプラグインに切り替えるために使用されます。 中間ソース管理アダプターパッケージに切り替えて、アクティブまたは非アクティブに設定する必要があるソース管理プラグインを特定するプロセスは、ユーザーに対して透過的です。 アダプターパッケージは、任意のソース管理プラグインがアクティブになっている場合、常にアクティブです。 プラグイン DLL を単に読み込んでアンロードするために、2つのソース管理プラグインを切り替える。 ただし、ソース管理 VSPackage に切り替えるには、IDE を操作して適切な VSPackage を読み込む必要があります。

 ソース管理 VSPackage は、ソリューションを開いたときに、VSPackage のレジストリキーがソリューションファイル内にある場合に呼び出されます。 ソリューションが開かれると、は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] レジストリ値を検索し、適切なソース管理 VSPackage を読み込みます。 すべてのソース管理 Vspackage には、上記で説明したレジストリエントリが必要です。 ソース管理下にあるソリューションは、特定のソース管理 VSPackage に関連付けられているとマークされています。 ソース管理 Vspackage は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> ソリューションベースの VSPackage の自動スワップを有効にするためにを実装する必要があります。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>パッケージの選択と切り替えを行うための Visual Studio UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**ソース管理カテゴリの** 下にある [**オプション**] ダイアログボックスで、ソース管理 VSPackage とプラグインを選択するための UI を提供します。 これにより、ユーザーはアクティブなソース管理プラグインまたは VSPackage を選択できます。 ドロップダウンリストには次のものが含まれます。

- インストールされているすべてのソース管理パッケージ

- インストールされているすべてのソース管理プラグイン

- "None" オプション。ソースコード管理を無効にします。

  アクティブなソース管理の選択肢の UI だけが表示されます。 VSPackage を選択すると、前の VSPackage の UI が非表示になり、新しい ui の UI が表示されます。 アクティブな VSPackage は、ユーザーごとに選択されます。 1人のユーザーが同時に開いている複数のコピーを同時に使用する場合 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、それぞれが異なるアクティブな VSPackage を使用する可能性があります。 複数のユーザーが同じコンピューターにログオンしている場合は、各ユーザーが個別のインスタンスを開くことができ [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、それぞれが異なる Active VSPackage を持ちます。 の複数のインスタンス [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] がユーザーによって閉じられると、最後に開いたソリューションに対してアクティブだったソース管理 VSPackage が既定のソース管理 VSPackage になり、再起動時にアクティブに設定されます。

  以前のバージョンのとは異なり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、IDE の再起動は、ソース管理の vspackage を切り替える唯一の方法ではなくなりました。 VSPackage の選択は自動的に行うことができます。 パッケージを切り替えるには、管理者またはパワーユーザーではなく、Windows ユーザー特権が必要です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [機能](../../extensibility/internals/source-control-vspackage-features.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
