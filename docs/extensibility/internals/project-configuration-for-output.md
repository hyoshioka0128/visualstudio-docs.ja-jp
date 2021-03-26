---
title: 出力のプロジェクト構成 |Microsoft Docs
description: 各構成がサポートできるビルドプロセス、および出力項目を使用できるようにするためのインターフェイスとメソッドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13e37999ad9f3bada375c1897207e1e4c15546e8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082011"
---
# <a name="project-configuration-for-output"></a>出力のためのプロジェクト構成
すべての構成で、実行可能ファイルやリソースファイルなどの出力項目を生成する一連のビルドプロセスをサポートできます。 これらの出力項目はユーザーに対してプライベートであり、実行可能ファイル (.exe、.dll、.lib) やソースファイル (.idl、.h ファイル) など、関連する種類の出力をリンクするグループに配置できます。

 出力項目は、メソッドを使用して取得 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> し、メソッドで列挙でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> ます。 出力項目をグループ化する場合は、プロジェクトでもインターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> ます。

 を実装することによって開発されたコンストラクトでは、 `IVsOutputGroup` プロジェクトが使用法に従って出力をグループ化できます。 たとえば、DLL がプログラムデータベース (PDB) と共にグループ化されている場合があります。

> [!NOTE]
> PDB ファイルにはデバッグ情報が含まれており、.dll または .exe をビルドするときに [デバッグ情報の生成] オプションを指定した場合に作成されます。 .Pdb ファイルは、通常、デバッグプロジェクト構成に対してのみ生成されます。

 グループ内に含まれる出力の数が構成によって異なる場合でも、プロジェクトはサポートされている構成ごとに同じ数のグループを返す必要があります。 たとえば、プロジェクトの mattd の DLL には、デバッグ構成で mattd.dll とが含まれている場合がありますが、リテール構成では matt.dll のみが含まれます。

 また、グループには、プロジェクト内の構成から構成まで、正規名、表示名、グループ情報など、同じ識別子情報が含まれています。 この一貫性により、構成が変更された場合でも、展開およびパッケージ化を継続できます。

 グループには、パッケージ化ショートカットが意味のあるものを指すようにするキー出力を含めることもできます。 特定の構成では、どのグループも空になる可能性があるため、グループのサイズについての前提条件を考慮する必要はありません。 構成に含まれる各グループのサイズ (出力の数) は、同じ構成内の別のグループのサイズとは異なる場合があります。 また、別の構成で同じグループのサイズと異なる場合もあります。

 ![出力グループグラフィック](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups") 出力グループ

 インターフェイスの主な用途 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> は、管理オブジェクトのビルド、配置、デバッグへのアクセスを提供し、プロジェクトが自由に出力をグループ化できるようにすることです。 このインターフェイスの使用方法の詳細については、「 [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)」を参照してください。

 上の図では、グループに組み込まれている構成 (bD.exe または b.exe) の間にキー出力があるため、ユーザーは、展開された構成に関係なく、ショートカットを作成して理解することができます。 グループソースにはキー出力がないため、ユーザーはそのショートカットを作成できません。 構築されたデバッググループにキー出力があり、構築された小売グループがない場合は、実装が正しくありません。 次に、いずれかの構成に出力が含まれていないグループがあり、その結果、キーファイルがない場合は、そのグループを持つその他の構成にキーファイルを含めることはできません。 インストーラーエディターでは、正規名とグループの表示名、およびキーファイルの存在は、構成に基づいて変更されないと想定しています。

 プロジェクトにパッケージ化または配置しないが含まれている場合は `IVsOutputGroup` 、その出力をグループに配置してはいけないことに注意してください。 出力は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> グループ化に関係なく、すべての構成の出力を返すメソッドを実装することで、通常どおり列挙できます。

 詳細については、「 `IVsOutputGroup` カスタムプロジェクトのサンプル」の「 [](https://github.com/tunnelvisionlabs/MPFProj10)の実装」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)
- [ビルドのためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)
- [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)
- [ソリューションの構成](../../extensibility/internals/solution-configuration.md)
