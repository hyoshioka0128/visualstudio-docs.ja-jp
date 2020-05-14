---
title: ソリューションの概要
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 767db749d953855cd5c6f81f356a195c830aa838
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705305"
---
# <a name="solutions-overview"></a>ソリューションの概要

ソリューションとは、アプリケーションを作成するために連携して動作する 1 つ以上のプロジェクトのグループです。 ソリューションに関連するプロジェクトと状態の情報は、2 つの異なるソリューション ファイルに格納されます。 [ソリューション (.sln) ファイル](solution-dot-sln-file.md)はテキスト ベースで、ソース コード管理の下に配置し、ユーザー間で共有できます。 [ソリューション ユーザー オプション (.suo) ファイル](solution-user-options-dot-suo-file.md)はバイナリです。 その結果、.suo ファイルはソース コード管理下に置かれなくなり、ユーザー固有の情報が含まれています。

どの VSPackage も、どちらの種類のソリューション ファイルにも書き込むことができます。 ファイルの性質上、書き込み用に実装された 2 つの異なるインターフェイスがあります。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>はテキスト情報を .sln ファイルに書<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>き込み、インターフェイスはバイナリ ストリームを .suo ファイルに書き込みます。

> [!NOTE]
> プロジェクトは、ソリューション ファイルに自分自身のエントリを明示的に書き込む必要はありません。環境は、プロジェクトの処理します。 したがって、ソリューション ファイルに特にコンテンツを追加する場合を除き、VSPackage をこの方法で登録する必要はありません。

各 VSPackage サポート ソリューションの永続化は<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>、3 つのインターフェイスを使用します、 インターフェイスは、環境によって実装され`IVsPersistSolutionProps`、VSPackage によって呼び出され、および`IVsPersistSolutionOpts`、両方の VSPackage によって実装されます。 インターフェイス`IVsPersistSolutionOpts`は、VSPackage によってプライベート情報が .suo ファイルに書き込まれる場合にのみ実装する必要があります。

ソリューションを開くと、次のプロセスが実行されます。

1. 環境はソリューションを読み取ります。

2. 環境が見つかった場合`CLSID`、対応する VSPackage が読み込まれます。

3. VSPackage が読み込まれている場合、`QueryInterface`環境<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>は、VSPackage が必要とするインターフェイスのインターフェイスを呼び出します。

   - sln ファイルから読み取るときに、環境`QueryInterface`は. `IVsPersistSolutionProps`

   - suo ファイルから読み取るとき、環境`QueryInterface`は. `IVsPersistSolutionOpts`

   これらのファイルの使用に関する具体的な情報は[、ソリューション (.Sln) ファイル](../../extensibility/internals/solution-dot-sln-file.md)および[ソリューションのユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md).

> [!NOTE]
> 2 つのプロジェクトの構成で構成され、ビルドから 3 つ目を除外する新しいソリューション構成を作成する場合は、プロパティ ページ UI またはオートメーションを使用する必要があります。 ソリューション ビルド マネージャーの構成とそのプロパティを直接変更することはできませんが、オートメーション モデルの DTE のクラス`SolutionBuild`を使用してソリューション ビルド マネージャーを操作できます。 ソリューションの構成の詳細については、「ソリューションの[構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
