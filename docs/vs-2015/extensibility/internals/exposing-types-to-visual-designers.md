---
title: ビジュアルデザイナーへの型の公開 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4d6c0e163b751f1873fdb941e85c273dcc4fde5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691203"
---
# <a name="exposing-types-to-visual-designers"></a>ビジュアル デザイナーへのタイプの公開
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ビジュアルデザイナーを表示するには、デザイン時にクラスと型の定義にアクセスできる必要があります。 クラスは、現在のプロジェクト (参照とその依存関係) の完全な依存関係セットを含む、定義済みのアセンブリセットから読み込まれます。 また、カスタムツールによって生成されるファイルで定義されているクラスや型にビジュアルデザイナーがアクセスする場合にも必要になることがあります。  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]およびプロジェクトシステムでは、 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 一時移植可能な実行可能ファイル (一時的な pe) を使用して、生成されたクラスと型にアクセスするためのサポートを提供しています。 カスタムツールによって生成されたすべてのファイルを一時アセンブリにコンパイルして、それらのアセンブリから型を読み込んでデザイナーに公開することができます。 各カスタムツールの出力は個別の一時 PE にコンパイルされ、この一時的なコンパイルの成功または失敗は、生成されたファイルをコンパイルできるかどうかによってのみ異なります。 プロジェクトが全体としてビルドされない場合でも、個々の一時 Pe は引き続きデザイナーで使用できます。  
  
 これらの変更がカスタムツールを実行した結果である場合、プロジェクトシステムは、カスタムツールの出力ファイルに対する変更の追跡を完全にサポートしています。 カスタムツールが実行されるたびに、新しい一時的な PE が生成され、適切な通知がデザイナーに送信されます。  
  
> [!NOTE]
> プログラム実行可能ファイルの一時生成ファイルはバックグラウンドで発生するため、コンパイルが失敗した場合、エラーはユーザーに報告されません。  
  
 一時的な PE サポートを利用するカスタムツールは、次の規則に従う必要があります。  
  
- `GeneratesDesignTimeSource` レジストリで1に設定する必要があります。  
  
     この設定がないと、プログラムの実行可能ファイルのコンパイルは行われません。  
  
- 生成されたコードは、グローバルプロジェクト設定と同じ言語である必要があります。  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>レジストリで1に設定されている要求された拡張機能がカスタムツールによって報告されるかどうかに関係なく、一時 PE がコンパイルされ `GeneratesDesignTimeSource` ます。 拡張子は .vb、.cs、または. jsl; である必要はありません。任意の拡張機能を使用できます。  
  
- カスタムツールによって生成されるコードは有効である必要があり、実行の完了時にプロジェクト内に存在する参照のセットだけを使用して、独自のコードをコンパイルする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> ます。  
  
     一時 PE がコンパイルされると、コンパイラに提供されるソースファイルは、カスタムツールの出力だけになります。 そのため、一時 PE を使用するカスタムツールでは、プロジェクト内の他のファイルとは別にコンパイルできる出力ファイルを生成する必要があります。  
  
## <a name="see-also"></a>参照  
 [BuildManager オブジェクトの概要](https://msdn.microsoft.com/50080ec2-c1c9-412c-98ef-18d7f895e7fa)   
 [単一ファイルジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)   
 [プロジェクトの既定の名前空間の決定](../../misc/determining-the-default-namespace-of-a-project.md)   
 [単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)
