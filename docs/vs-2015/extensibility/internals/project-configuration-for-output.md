---
title: 出力のプロジェクト構成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: addd7e8630ce35c6bdbbbb4c063197f75a74c97d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300677"
---
# <a name="project-configuration-for-output"></a>出力のためのプロジェクト構成
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

すべての構成で、実行可能ファイルやリソースファイルなどの出力項目を生成する一連のビルドプロセスをサポートできます。 これらの出力項目はユーザーに対してプライベートであり、実行可能ファイル (.exe、.dll、.lib) やソースファイル (.idl、.h ファイル) など、関連する種類の出力をリンクするグループに配置できます。  
  
 出力項目は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> メソッドを使用して取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> メソッドで列挙できます。 出力項目をグループ化する場合は、プロジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> インターフェイスも実装する必要があります。  
  
 `IVsOutputGroup` の実装によって開発されたコンストラクトでは、プロジェクトが使用法に従って出力をグループ化できます。 たとえば、DLL がプログラムデータベース (PDB) と共にグループ化されている場合があります。  
  
> [!NOTE]
> PDB ファイルにはデバッグ情報が含まれており、.dll または .exe をビルドするときに [デバッグ情報の生成] オプションを指定した場合に作成されます。 .Pdb ファイルは、通常、デバッグプロジェクト構成に対してのみ生成されます。  
  
 グループ内に含まれる出力の数が構成によって異なる場合でも、プロジェクトはサポートされている構成ごとに同じ数のグループを返す必要があります。 たとえば、プロジェクトの mattd と mattd は、デバッグ構成に含まれる場合がありますが、リテール構成に含まれるのはその dll のみです。  
  
 また、グループには、プロジェクト内の構成から構成まで、正規名、表示名、グループ情報など、同じ識別子情報が含まれています。 この一貫性により、構成が変更された場合でも、展開およびパッケージ化を継続できます。  
  
 グループには、パッケージ化ショートカットが意味のあるものを指すようにするキー出力を含めることもできます。 特定の構成では、どのグループも空になる可能性があるため、グループのサイズについての前提条件を考慮する必要はありません。 構成に含まれる各グループのサイズ (出力の数) は、同じ構成内の別のグループのサイズとは異なる場合があります。 また、別の構成で同じグループのサイズと異なる場合もあります。  
  
 ![出力グループグラフィック](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups")  
出力グループ  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> インターフェイスの主な用途は、管理オブジェクトのビルド、配置、デバッグへのアクセスを提供し、プロジェクトが自由に出力をグループ化できるようにすることです。 このインターフェイスの使用方法の詳細については、「[プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)」を参照してください。  
  
 上の図では、構築されたグループが構成全体にわたってキー出力を持っています (Bd-re または b .exe)。これにより、ユーザーは、展開された構成に関係なく、ショートカットを作成して使用できることを理解できます。 グループソースにはキー出力がないため、ユーザーはそのショートカットを作成できません。 構築されたデバッググループにキー出力があり、構築された小売グループがない場合は、実装が正しくありません。 次に、いずれかの構成に出力が含まれていないグループがあり、その結果、キーファイルがない場合は、そのグループを持つその他の構成にキーファイルを含めることはできません。 インストーラーエディターでは、正規名とグループの表示名、およびキーファイルの存在は、構成に基づいて変更されないと想定しています。  
  
 プロジェクトにパッケージ化または配置しない `IVsOutputGroup` が含まれている場合は、その出力をグループに配置してはいけないことに注意してください。 出力は、グループ化に関係なくすべての構成の出力を返す <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> メソッドを実装することで、通常どおり列挙できます。  
  
 詳細については、「カスタムプロジェクト[の](https://archive.codeplex.com/?p=mpfproj12)サンプル」の「`IVsOutputGroup` の実装」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [構成オプションの管理](../../extensibility/internals/managing-configuration-options.md)   
  [をビルドするためのプロジェクト構成](../../extensibility/internals/project-configuration-for-building.md)  
 [プロジェクト構成オブジェクト](../../extensibility/internals/project-configuration-object.md)   
 [ソリューション構成](../../extensibility/internals/solution-configuration.md)
