---
title: 出力用プロジェクト構成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78b95457af4c5d806fdfcc20f49ac4e82df36488
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706667"
---
# <a name="project-configuration-for-output"></a>出力のためのプロジェクト構成
すべての構成では、実行可能ファイルやリソース ファイルなどの出力項目を生成するビルド プロセスのセットをサポートできます。 これらの出力項目はユーザー専用であり、実行可能ファイル (.exe、.dll、.lib) やソース ファイル (.idl、.h ファイル) などの関連する種類の出力をリンクするグループに配置できます。

 出力項目は<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2>メソッドを使用して使用できるようにし、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>メソッドを列挙できます。 出力項目をグループ化する場合は、プロジェクトにもインターフェイスを実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>する必要があります。

 実装`IVsOutputGroup`によって開発されたコンストラクトは、プロジェクトが使用法に従って出力をグループ化できるようにします。 たとえば、DLL はプログラム データベース (PDB) とグループ化されます。

> [!NOTE]
> PDB ファイルにはデバッグ情報が含まれ、.dll または .exe のビルド時に [デバッグ情報の生成] オプションが指定されたときに作成されます。 pdb ファイルは、通常、デバッグ プロジェクト構成のためだけに生成されます。

 プロジェクトは、グループ内の出力数が構成によって異なる場合がある場合でも、サポートする構成ごとに同じ数のグループを返す必要があります。 たとえば、プロジェクト Matt の DLL には、デバッグ構成に mattd.dll と mattd.pdb が含まれますが、Retail 構成には matt.dll のみが含まれます。

 また、グループには、プロジェクト内の構成から構成まで、正規名、表示名、グループ情報など、同じ識別子情報が含まれます。 この一貫性により、構成が変更されても展開とパッケージ化は引き続き動作します。

 グループには、パッケージングショートカットが意味のある何かを指すことができる重要な出力を持つことができます。 グループは、特定の構成で空になる可能性があるため、グループのサイズに関する想定は行いません。 構成の各グループのサイズ (出力数) は、同じ構成内の別のグループのサイズとは異なる場合があります。 また、別の構成で同じグループのサイズと異なる場合もあります。

 ![出力グループグラフィック](../../extensibility/internals/media/vsoutputgroups.gif "グループ化")出力グループ

 このインターフェイスの<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg>主な用途は、管理オブジェクトのビルド、配置、デバッグへのアクセスを提供し、プロジェクトが出力をグループ化する自由を可能にすることです。 このインターフェイスの使用方法の詳細については、「[プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)」を参照してください。

 前の図では、グループ構築は、構成 (bD.exe または b.exe) 間で重要な出力を持っているので、ユーザーは構築へのショートカットを作成し、展開された構成に関係なく、ショートカットが機能することを確認できます。 グループソースにはキー出力が存在しないため、ユーザーはそれにショートカットを作成できません。 ビルドされたデバッグ グループに重要な出力があるが、Retail グループがビルドしない場合、それは誤った実装になります。 次に、いずれかの構成に出力を含まないグループがあり、その結果、キー・ファイルがない場合、そのグループに出力を含むその他の構成はキー・ファイルを持つことができないという。 インストーラー・エディターは、正規名とグループの表示名、およびキー・ファイルの存在は、構成に基づいて変更されないと想定しています。

 プロジェクトにパッケージ化または展開を`IVsOutputGroup`行いたくないというものがある場合は、その出力をグループに入れないようにするだけで十分です。 グループ化に関係なく、構成のすべての出力を返す<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A>メソッドを実装することで、出力を通常どおりに列挙できます。

 詳細については、「 プロジェクトの MPF のカスタム プロジェクトサンプル 」の実装`IVsOutputGroup`[を参照してください](https://github.com/tunnelvisionlabs/MPFProj10)。

## <a name="see-also"></a>関連項目
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューション構成](../../extensibility/internals/solution-configuration.md)
