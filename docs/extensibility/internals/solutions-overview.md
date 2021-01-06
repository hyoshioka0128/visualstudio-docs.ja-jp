---
title: ソリューションの概要
description: ソリューションの内部について説明します。拡張機能の開発者は、Visual Studio 拡張機能でソリューションを使用することをお勧めします。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b2888f2fd0b2c9b7bfb530cc3fd46708ca13422f
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876728"
---
# <a name="solutions-overview"></a>ソリューションの概要

ソリューションは、アプリケーションを作成するために連携して動作する1つ以上のプロジェクトをグループ化したものです。 ソリューションに関連するプロジェクトと状態の情報は、2つの異なるソリューションファイルに格納されます。 [ソリューション (.sln) ファイル](solution-dot-sln-file.md)はテキストベースであり、ソースコード管理の下に配置し、ユーザー間で共有できます。 [ソリューションユーザーオプション (.suo) ファイル](solution-user-options-dot-suo-file.md)はバイナリです。 そのため、.suo ファイルをソースコード管理下に配置し、ユーザー固有の情報を含めることはできません。

どの VSPackage も、いずれかの種類のソリューションファイルに書き込むことができます。 ファイルの性質により、2つの異なるインターフェイスが実装され、それらに書き込むことができます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> テキスト情報を .sln ファイルに書き込みます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> インターフェイスは、.suo ファイルにバイナリストリームを書き込みます。

> [!NOTE]
> プロジェクトは、それ自体のエントリをソリューションファイルに明示的に書き込む必要はありません。環境では、プロジェクトに対してこれを処理します。 そのため、特にソリューションファイルにコンテンツを追加する必要がない場合は、この方法で VSPackage を登録する必要はありません。

ソリューションの永続化をサポートする各 VSPackage は、インターフェイスである3つのインターフェイスを使用します。このインターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 環境によって実装され、VSPackage によって呼び出され `IVsPersistSolutionProps` `IVsPersistSolutionOpts` ます。また、VSPackage によって実装されるともあります。 インターフェイスを実装する必要があるのは `IVsPersistSolutionOpts` 、VSPackage によって、.suo ファイルにプライベート情報が書き込まれる場合だけです。

ソリューションを開くと、次の処理が行われます。

1. 環境によってソリューションが読み取られます。

2. 環境でが検出されると、 `CLSID` 対応する VSPackage が読み込まれます。

3. VSPackage が読み込まれる場合、環境は `QueryInterface` 、VSPackage が必要とするインターフェイスのインターフェイスを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。

   - .Sln ファイルから読み取る場合、環境は `QueryInterface` を呼び出し `IVsPersistSolutionProps` ます。

   - .Suo ファイルから読み取る場合、環境は `QueryInterface` を呼び出し `IVsPersistSolutionOpts` ます。

   これらのファイルの使用に関する具体的な情報については、 [「ソリューション (」を参照してください。Sln) ファイル](../../extensibility/internals/solution-dot-sln-file.md) と [ソリューションのユーザーオプション ().Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

> [!NOTE]
> 2つのプロジェクトの構成で構成され、3番目の構成をビルドから除外する新しいソリューション構成を作成する場合は、プロパティページの UI またはオートメーションを使用する必要があります。 ソリューションビルドマネージャーの構成とそのプロパティを直接変更することはできませんが、オートメーションモデルの DTE のクラスを使用してソリューションビルドマネージャーを操作でき `SolutionBuild` ます。 ソリューションの構成の詳細については、「 [ソリューションの構成](../../extensibility/internals/solution-configuration.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
