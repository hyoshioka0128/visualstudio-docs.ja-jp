---
title: ファイル名拡張子の動詞を登録する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ac2854f1799075cc14d9beb557335be5228be21d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701534"
---
# <a name="register-verbs-for-file-name-extensions"></a>ファイル名拡張子の動詞を登録する
ファイル名拡張子とアプリケーションの関連付けには、通常、ユーザーがファイルをダブルクリックしたときに実行される推奨アクションがあります。 この優先アクションは、アクションに対応する動詞 (たとえば、オープン) にリンクされます。

 **progid}\shell\{** にあるシェル キーを使用して、拡張機能のプログラム識別子 (ProgID) に関連付けられている動詞HKEY_CLASSES_ROOT登録できます。 詳細については、[ファイルの種類を](/windows/desktop/shell/fa-file-types)参照してください。

## <a name="register-standard-verbs"></a>標準動詞の登録
 オペレーティング システムは、次の標準動詞を認識します。

- [ファイル]

- [編集]

- [再生]

- Print

- プレビュー

  可能な限り、標準動詞を登録します。 最も一般的な選択肢は、Open 動詞です。 編集動詞は、ファイルを開くこととファイルを編集する場合に明確な違いがある場合にのみ使用します。 たとえば *、.htm*ファイルを開くとブラウザに表示され *、.htm*ファイルを編集すると HTML エディタが起動します。 標準動詞は、オペレーティング システムのロケールにローカライズされます。

> [!NOTE]
> 標準動詞を登録する場合は、Open キーの既定値を設定しないでください。 既定値には、メニューの表示文字列が含まれています。 オペレーティング システムは、標準の動詞にこの文字列を提供します。

 プロジェクト ファイルは、ユーザー[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]がファイルを開いたときに新しいインスタンスを開始するために登録する必要があります。 プロジェクトの標準動詞登録の例を次に[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]示します。

```
[HKEY_CLASSES_ROOT\.csproj]
@="VisualStudio.csproj.8.0"

[HKEY_CLASSES_ROOT\.csproj\OpenWithList]
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]
@=""

[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]
"VisualStudio.csproj.8.0"=""

[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]
@="C# Project file"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""
```

 の既存の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]インスタンスでファイルを開くには、DDEEXEC キーを登録します。 次の例は[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]*、.cs*ファイルの標準の動詞登録を示しています。

```
[HKEY_CLASSES_ROOT\.cs]
@="VisualStudio.cs.8.0"

[HKEY_CLASSES_ROOT\.cs\OpenWithList]
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]
@=""

[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]
"VisualStudio.cs.8.0"=""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]
@="C# Source file"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]
@="Open(\"%1\")"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]
@="VisualStudio.8.0"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]
@="system"
```

## <a name="set-the-default-verb"></a>既定の動詞を設定する
 既定の動詞は、ユーザーが Windows エクスプローラーでファイルをダブルクリックしたときに実行されるアクションです。 既定の動詞は **、HKEY_CLASSES_ROOT\\*progid*\Shell**キーの既定値として指定された動詞です。 値を指定しない場合、既定の動詞は **、HKEY_CLASSES_ROOT\\*progid*\Shell**キー リストで指定された最初の動詞です。

> [!NOTE]
> side-by-side 展開で拡張機能の既定の動詞を変更する場合は、インストールと削除への影響を考慮してください。 インストール中に、元のデフォルト値が上書きされます。

## <a name="see-also"></a>関連項目
- [ファイルの関連付けを管理する](../extensibility/managing-side-by-side-file-associations.md)
