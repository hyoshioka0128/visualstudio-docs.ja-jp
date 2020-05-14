---
title: ビジュアル デザイナへの型の公開 |マイクロソフトドキュメント
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
ms.openlocfilehash: 9067f88b4bf1334e23a548bc6a2cbeb3eac6ad33
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708434"
---
# <a name="expose-types-to-visual-designers"></a>ビジュアル デザイナーに型を公開する
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ビジュアル デザイナーを表示するには、デザイン時にクラスおよび型の定義にアクセスできる必要があります。 クラスは、現在のプロジェクトの完全な依存関係セット (参照とその依存関係) を含む定義済みのアセンブリ セットから読み込まれます。 ビジュアル デザイナーがカスタム ツールによって生成されたファイルで定義されているクラスや型にアクセスする必要がある場合もあります。

 および[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)][!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]プロジェクト システムは、一時的なポータブル実行可能ファイル (一時ファイル ) を使用して生成されたクラスおよび型にアクセスするためのサポートを提供します。 カスタム ツールによって生成されたファイルは、型がアセンブリから読み込まれ、デザイナーに公開されるように、一時アセンブリにコンパイルできます。 各カスタム ツールの出力は個別の一時 PE にコンパイルされ、この一時コンパイルの成功または失敗は、生成されたファイルをコンパイルできるかどうかによってのみ異なります。 プロジェクト全体がビルドされない場合でも、個々の一時的な ES はデザイナーが利用できる場合があります。

 プロジェクト システムは、カスタム ツールの実行結果が変更された場合に、カスタム ツールの出力ファイルに対する変更を追跡するための完全なサポートを提供します。 カスタム ツールが実行されるたびに、新しい一時的な PE が生成され、適切な通知がデザイナーに送信されます。

> [!NOTE]
> プログラムの実行可能ファイルはバックグラウンドで実行されるため、コンパイルに失敗してもエラーは報告されません。

 一時的な PE サポートを利用するカスタム ツールは、次の規則に従う必要があります。

- レジストリ**で 1**に設定する必要があります。

     プログラムの実行可能ファイルのコンパイルは、この設定なしで実行されません。

- 生成されるコードは、グローバル プロジェクト設定と同じ言語である必要があります。

     一時的な PE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>**カスタム**ツールが要求された拡張機能として報告するものに関係なくコンパイルされます。 拡張子は *.vb* *、.cs*、または *.jsl*である必要はありません。任意の拡張子を指定できます。

- カスタム ツールによって生成されるコードは有効である必要があり、実行が終了した時点<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>でプロジェクトに存在する参照のセットのみを使用してコンパイルする必要があります。

     一時的な PE がコンパイルされるとき、コンパイラに提供されるソース ファイルはカスタム ツール出力だけです。 したがって、一時的な PE を使用するカスタム ツールは、プロジェクト内の他のファイルとは独立してコンパイルできる出力ファイルを生成する必要があります。

## <a name="see-also"></a>関連項目
- [ビルド マネージャ オブジェクトの概要](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)
- [単一ファイル ジェネレータの登録](../../extensibility/internals/registering-single-file-generators.md)
