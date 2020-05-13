---
title: サイド バイ サイド ファイルの関連付けを管理する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6c284fe7ef4c2d07051a8524860583cb634e13bf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702758"
---
# <a name="manage-side-by-side-file-associations"></a>ファイルの関連付けを管理する

VSPackage がファイルの関連付けを提供する場合は、ファイルを開くために特定の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]バージョンを呼び出す必要があるサイド バイ サイド インストールを処理する方法を決定する必要があります。 互換性のないファイル形式は、問題を複雑にします。

ユーザーは、新しいバージョンの製品が以前のバージョンと互換性を持っていることを期待するため、既存のファイルをデータを失うことなく新しいバージョンにロードできます。 理想的には、VSPackage は、読み込みと以前のバージョンのファイル形式を保存できます。 これが true でない場合は、VSPackage の新しいバージョンにファイル形式をアップグレードする必要があります。 この方法の欠点は、アップグレードされたファイルを以前のバージョンで開くことができないということです。

この問題を回避するには、ファイル形式が互換性のない場合に拡張子を変更します。 たとえば、VSPackage のバージョン 1 では拡張子 *.mypkg10*を使用でき、バージョン 2 では拡張子 *.mypkg20*を使用できます。 この違いは、特定のファイルを開く VSPackage を識別します。 古い拡張子に関連付けられているプログラムの一覧に新しい VSPackages を追加する場合、ユーザーはファイルを右クリックして、新しい VSPackage で開くことを選択できます。 その時点で、VSPackage は、新しい形式にファイルをアップグレードするか、ファイルを開くし、VSPackage の以前のバージョンとの互換性を維持する提供できます。

> [!NOTE]
> これらのアプローチを組み合わせることができます。 たとえば、古いファイルを読み込むことで下位互換性を提供し、ユーザーがファイル形式を保存するときにファイル形式をアップグレードするように指定できます。

## <a name="face-the-problem"></a>問題に直面する

複数のサイド バイ サイド VSPackages で同じ拡張子を使用する場合は、その拡張子[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に関連付けられているバージョンを選択する必要があります。 次の 2 つの方法があります。

- ユーザーのコンピュータにインストールされている最新バージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]のファイルを開きます。

   この方法では、インストーラーは、ファイルの関連付け用に書[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]き込まれたレジストリ エントリの最新バージョンを決定します。 Windows インストーラ パッケージには、カスタム動作を含めるで、最新バージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を示すプロパティを設定できます。

  > [!NOTE]
  > このコンテキストでは、「最新」は「最新のサポートされているバージョン」を意味します。 これらのインストーラー エントリは、それ以降のリリースの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を自動的に検出しません。 [システム要件の検出](../extensibility/internals/detecting-system-requirements.md)と[インストール後に実行する必要があるコマンド](../extensibility/internals/commands-that-must-be-run-after-installation.md)のエントリは、ここで示したものと似ており、追加バージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]をサポートするために必要です。

   CustomAction テーブルの次の行は、DEVENV_EXE_LATEST プロパティを設定し、[インストール後に実行する必要があるコマンド](../extensibility/internals/commands-that-must-be-run-after-installation.md)で説明した AppSearch テーブルと RegLocator テーブルで設定されたプロパティにします。 テーブルの行は、実行シーケンスの初期段階でカスタム アクションをスケジュールします。 [条件] 列の値によって、ロジックが機能します。

  - Visual Studio .NET 2002 は、現在のバージョンが唯一の場合は最新バージョンです。

  - Visual Studio .NET 2003 は、最新バージョンが存在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]し、存在しない場合にのみ使用されます。

  - [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]は、現在のバージョンが唯一の場合は最新バージョンです。

    結果として、DEVENV_EXE_LATESTに最新バージョンの devenv.exe のパスが含まれるという結果が得られます。

  **最新バージョンの Visual Studio を決定するカスタム アクション テーブル行**

  |アクション|Type|source|移行先|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **Visual Studio の最新バージョンを決定するテーブル行のインストール実行シーケンス**

  |アクション|条件|Sequence|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002としない(DEVENV_EXE_2003またはDEVENV_EXE_2005)|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003とDEVENV_EXE_2005ではない|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   Windows インストーラ パッケージのレジストリ テーブルのDEVENV_EXE_LATEST プロパティを使用して **、HKEY_CLASSES_ROOT*ProgId*ShellOpenCommand**キーの既定値 [DEVENV_EXE_LATEST] "%1" を書き込むことができます。

- 利用可能な VSPackage バージョンから最良の選択を行うことができる共有ランチャー プログラムを実行します。

   開発者は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]このアプローチを選択して、多くのバージョンの ソリューションおよびプロジェクトの複数の形式の複雑な要件[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を処理します。 この方法では、ランチャー プログラムを拡張機能ハンドラーとして登録します。 ランチャーはファイルを調べ、VSPackage のどのバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]がその特定のファイルを処理できるかを決定します。 たとえば、ユーザーが VSPackage の特定のバージョンで最後に保存されたファイルを開いた場合、ランチャーは、対応するバージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage を起動できます。 さらに、ユーザーは常に最新バージョンを起動するようにランチャーを構成できます。 ランチャーは、ファイルの形式をアップグレードするようにユーザーに促すこともできます。 ファイルの形式にバージョン番号が含まれている場合、ファイル形式がインストールされている VSPackages の 1 つ以上のバージョンからのファイル形式かどうかをユーザーに通知できます。

   起動ツールは、VSPackage のすべてのバージョンと共有される Windows インストーラー コンポーネントに含まれている必要があります。 このプロセスにより、最新バージョンが常にインストールされ、VSPackage のすべてのバージョンがアンインストールされるまで削除されません。 この方法では、VSPackage の 1 つのバージョンがアンインストールされた場合でも、ランチャー コンポーネントのファイルの関連付けやその他のレジストリ エントリが保持されます。

## <a name="uninstall-and-file-associations"></a>アンインストールとファイルの関連付け

ファイルの関連付けのレジストリ エントリを書き込む VSPackage をアンインストールすると、ファイルの関連付けが削除されます。 したがって、拡張機能には関連付けられたプログラムはありません。 Windows インストーラーは、VSPackage のインストール時に追加されたレジストリ エントリを "回復" しません。 ユーザーのファイルの関連付けを修正する方法を次に示します。

- 前述のとおり、共有ランチャーコンポーネントを使用します。

- ユーザーがファイルの関連付けを所有する VSPackage のバージョンの修復を実行するようにユーザーに指示します。

- 適切なレジストリ エントリを書き換える別の実行可能プログラムを提供します。

- ユーザーがファイルの関連付けを選択し、失われた関連付けを再利用できるようにする構成オプション ページまたはダイアログ ボックスを提供します。 アンインストール後に実行するようユーザーに指示します。

## <a name="see-also"></a>関連項目

- [サイド バイ サイド展開のファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [ファイル名拡張子の動詞を登録する](../extensibility/registering-verbs-for-file-name-extensions.md)
