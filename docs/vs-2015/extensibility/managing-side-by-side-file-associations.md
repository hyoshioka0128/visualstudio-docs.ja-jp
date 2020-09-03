---
title: Side-by-side ファイルの関連付けの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b8ca68aec180c51a170fd6ecce58237a5b306705
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194394"
---
# <a name="managing-side-by-side-file-associations"></a>side-by-side のファイルの関連付けを管理する

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage がファイルの関連付けを提供する場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ファイルを開くために特定のバージョンのを呼び出す必要があるサイドバイサイドインストールをどのように処理するかを決定する必要があります。 互換性のないファイル形式は、問題を複合します。

ユーザーは、新しいバージョンの製品を以前のバージョンと互換性があると想定しているため、既存のファイルを新しいバージョンに読み込んでデータを失うことはありません。 VSPackage を使用すると、以前のバージョンのファイル形式を読み込んで保存することができます。 それが当てはまる場合は、ファイル形式を VSPackage の新しいバージョンにアップグレードすることをお勧めします。 この方法の欠点は、アップグレードされたファイルを以前のバージョンで開くことができないことです。

この問題を回避するには、ファイル形式に互換性がなくなったときに拡張機能を変更します。 たとえば、VSPackage のバージョン1では拡張子 mypkg10 を使用し、バージョン2では拡張子 mypkg20 を使用できます。 この違いにより、特定のファイルを開く VSPackage が識別されます。 古い拡張機能に関連付けられているプログラムの一覧に新しい Vspackage を追加した場合、ユーザーはファイルを右クリックして、新しい VSPackage で開くことができます。 この時点で、VSPackage は、ファイルを新しい形式にアップグレードするか、ファイルを開いて、以前のバージョンの VSPackage との互換性を維持することを提供できます。

> [!NOTE]
> これらのアプローチを組み合わせることができます。 たとえば、古いファイルを読み込んで旧バージョンとの互換性を提供し、ユーザーが保存したときにファイル形式をアップグレードすることができます。

## <a name="facing-the-problem"></a>問題に直面しています

複数のサイドバイサイド Vspackage で同じ拡張機能を使用する場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能に関連付けられているのバージョンを選択する必要があります。 次の2つの選択肢があります。

- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]ユーザーのコンピューターにインストールされているの最新バージョンでファイルを開きます。

   この方法では、インストーラーは、の最新バージョンを確認 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] し、ファイルの関連付け用に記述されたレジストリエントリにそれを含めます。 Windows インストーラーパッケージでは、の最新バージョンを示すプロパティを設定するカスタムアクションを含めることができ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

  > [!NOTE]
  > このコンテキストでは、"latest" は "最新のサポートされているバージョン" を意味します。 これらのインストーラーエントリは、の今後のリリースを自動的に検出しません [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。 [インストール後に実行する必要](../extensibility/internals/commands-that-must-be-run-after-installation.md)がある[システム要件](../extensibility/internals/detecting-system-requirements.md)とコマンドの検出のエントリは、ここに記載されているものと似ており、の追加バージョンをサポートするために必要です [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

   CustomAction テーブルの次の行は、DEVENV_EXE_LATEST プロパティを、「 [インストール後に実行する必要のあるコマンド](../extensibility/internals/commands-that-must-be-run-after-installation.md)」で説明されている AppSearch および reglocator テーブルによって設定されるプロパティに設定します。 InstallExecuteSequence テーブル内の行は、実行シーケンスの早い段階でカスタムアクションをスケジュールします。 条件列の値によって、ロジックが機能します。

  - Visual Studio .NET 2002 は、唯一のバージョンの場合は、最新バージョンです。

  - Visual Studio .NET 2003 は、現在のバージョンであり、存在しない場合にのみ、最新のバージョンです [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

  - [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は最新バージョンであり、唯一のバージョンです。

    結果として、DEVENV_EXE_LATEST には devenv.exe の最新バージョンのパスが含まれます。

  **CustomAction Visual Studio の最新バージョンを決定するテーブル行**

  |アクション|Type|source|移行先|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **Visual Studio の最新バージョンを決定する InstallExecuteSequence テーブル行**

  |アクション|条件|シーケンス|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 と NOT (DEVENV_EXE_2003 または DEVENV_EXE_2005)|410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 であり DEVENV_EXE_2005 ではありません|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   Windows インストーラーパッケージのレジストリテーブルの DEVENV_EXE_LATEST プロパティを使用して、HKEY_CLASSES_ROOT*ProgId*ShellOpenCommand キーの既定値である [DEVENV_EXE_LATEST] "%1" を書き込むことができます。

- 使用可能な VSPackage バージョンから最適な選択を行うことができる共有ランチャープログラムを実行します。

   の開発者は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] この方法を選択して、多くのバージョンので発生する複数の形式のソリューションとプロジェクトの複雑な要件を処理し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 この方法では、ランチャープログラムを拡張機能ハンドラーとして登録します。 ランチャーは、ファイルを調べ、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] その特定のファイルを処理できるのバージョンと VSPackage を決定します。 たとえば、特定のバージョンの VSPackage によって最後に保存されたファイルをユーザーが開いた場合、ランチャーは、対応するバージョンのでその VSPackage を開始でき [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 また、ユーザーはランチャーを構成して常に最新バージョンを起動することもできます。 ランチャーでは、ファイルの形式をアップグレードするようにユーザーに求めることもできます。 ファイルの形式にバージョン番号が含まれている場合、ランチャーは、インストールされている Vspackage のうちの1つ以上のバージョンのファイル形式であるかどうかをユーザーに通知できます。

   ランチャーは、VSPackage のすべてのバージョンと共有される Windows インストーラーコンポーネントに含まれている必要があります。 このプロセスによって、最新バージョンが常にインストールされ、VSPackage のすべてのバージョンがアンインストールされるまで削除されません。 この方法では、VSPackage の1つのバージョンがアンインストールされても、ランチャーコンポーネントのファイルの関連付けとその他のレジストリエントリは保持されます。

## <a name="uninstall-and-file-associations"></a>アンインストールとファイルの関連付け

ファイルの関連付けのレジストリエントリを書き込む VSPackage をアンインストールすると、ファイルの関連付けが削除されます。 そのため、拡張機能に関連付けられているプログラムはありません。 Windows インストーラーは、VSPackage のインストール時に追加されたレジストリエントリを "回復" しません。 ユーザーのファイルの関連付けを修正するには、次の方法があります。

- 前述のように、共有ランチャーコンポーネントを使用します。

- ユーザーがファイルの関連付けを所有する VSPackage のバージョンの修復を実行するように指示します。

- 適切なレジストリエントリを書き換える別の実行可能プログラムを指定します。

- [構成オプション] ページまたはダイアログボックスを使用して、ユーザーがファイルの関連付けを選択し、失われた関連付けを再利用できるようにします。 アンインストール後に実行するようにユーザーに指示します。

## <a name="see-also"></a>参照

[サイドバイサイド配置のためにファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) 
[ファイル名拡張子に対する動詞の登録](../extensibility/registering-verbs-for-file-name-extensions.md)
