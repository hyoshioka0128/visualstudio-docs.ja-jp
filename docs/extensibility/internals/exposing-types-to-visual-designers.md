---
title: ビジュアルデザイナーへの型の公開 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 48aa8a729b5cc38d3cee08a7f5ec143d5e84931a
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012531"
---
# <a name="expose-types-to-visual-designers"></a>ビジュアルデザイナーに型を公開する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ビジュアルデザイナーを表示するには、デザイン時にクラスと型の定義にアクセスできる必要があります。 クラスは、現在のプロジェクト (参照とその依存関係) の完全な依存関係セットを含む、定義済みのアセンブリセットから読み込まれます。 また、カスタムツールによって生成されるファイルで定義されているクラスや型にビジュアルデザイナーがアクセスする場合にも必要になることがあります。

 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]およびプロジェクトシステムでは、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 一時移植可能な実行可能ファイル (一時的な pe) を使用して、生成されたクラスと型にアクセスするためのサポートを提供しています。 カスタムツールによって生成されたすべてのファイルを一時アセンブリにコンパイルして、それらのアセンブリから型を読み込んでデザイナーに公開することができます。 各カスタムツールの出力は個別の一時 PE にコンパイルされ、この一時的なコンパイルの成功または失敗は、生成されたファイルをコンパイルできるかどうかによってのみ異なります。 プロジェクトが全体としてビルドされない場合でも、個々の一時 Pe は引き続きデザイナーで使用できる可能性があります。

 これらの変更がカスタムツールを実行した結果である場合、プロジェクトシステムは、カスタムツールの出力ファイルに対する変更の追跡を完全にサポートしています。 カスタムツールが実行されるたびに、新しい一時的な PE が生成され、適切な通知がデザイナーに送信されます。

> [!NOTE]
> プログラム実行可能ファイルの一時生成ファイルはバックグラウンドで発生するため、コンパイルが失敗した場合、エラーはユーザーに報告されません。

 一時的な PE サポートを利用するカスタムツールは、次の規則に従う必要があります。

- レジストリで**GeneratesDesignTimeSource**を1に設定する必要があります。

     この設定がないと、プログラムの実行可能ファイルのコンパイルは行われません。

- 生成されたコードは、グローバルプロジェクト設定と同じ言語である必要があります。

     <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>レジストリで**GeneratesDesignTimeSource**が1に設定されている場合、カスタムツールが要求された拡張機能として報告する内容に関係なく、一時 PE がコンパイルされます。 拡張子は *.vb*、 *.cs*、または *. jsl*; である必要はありません。任意の拡張機能を使用できます。

- カスタムツールによって生成されるコードは有効である必要があり、実行の完了時にプロジェクト内に存在する参照のセットだけを使用して、独自のコードをコンパイルする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> ます。

     一時 PE がコンパイルされると、コンパイラに提供されるソースファイルは、カスタムツールの出力だけになります。 そのため、一時 PE を使用するカスタムツールでは、プロジェクト内の他のファイルとは別にコンパイルできる出力ファイルを生成する必要があります。

## <a name="see-also"></a>関連項目
- [BuildManager オブジェクトの概要](/previous-versions/8f9kffa8(v=vs.140))
- [単一ファイルジェネレーターを実装する](../../extensibility/internals/implementing-single-file-generators.md)
- [単一ファイルジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)