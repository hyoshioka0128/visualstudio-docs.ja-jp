---
title: ビジュアルスタジオの階層 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cdbb8a0e58f6b1e5bc6e32f8c319d1480c4db4b5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708182"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio での階層
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) では、プロジェクトが*階層*として表示されます。 IDE では、階層はノードのツリーであり、各ノードには一連の関連付けられたプロパティがあります。 *プロジェクト階層*は、プロジェクトの項目、項目の関係、および項目の関連するプロパティとコマンドを保持するコンテナーです。

 では[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、階層インタフェース を使用してプロジェクト階層を管理<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>します。 インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>は、プロジェクト項目から呼び出すコマンドを、標準コマンド ハンドラーではなく適切な階層ウィンドウにリダイレクトします。

## <a name="project-hierarchies"></a>プロジェクト階層
 各プロジェクト階層には、表示および編集できる項目が含まれています。 これらの項目は、プロジェクトの種類によって異なります。 たとえば、データベース プロジェクトには、ストアド プロシージャ、データベース ビュー、およびデータベース テーブルが含まれる場合があります。 プログラミング言語プロジェクトには、ビットマップやダイアログ ボックス用のソース ファイルやリソース ファイルが含まれる可能性があります。 階層は入れ子にすることができ、プロジェクト階層を作成するときに柔軟性を高めることができます。

 新しいプロジェクトタイプを作成すると、プロジェクトタイプで編集できる項目の完全なセットが制御されます。 ただし、プロジェクトには編集サポートがない項目を含めることができます。 たとえば、Visual C++ プロジェクトには、HTML ファイルの種類に合わせてカスタマイズされたエディターが用意されていない場合でも、HTML ファイルを含めることができます。

 階層は、階層に含まれるアイテムの永続性を管理します。 階層の実装は、階層内の項目の永続性に影響を与える特別なプロパティを制御する必要があります。 たとえば、項目がファイルではなくリポジトリ内のオブジェクトを表す場合、階層の実装は、それらのオブジェクトの永続性を制御する必要があります。 IDE 自体は、ユーザー入力に対応して項目を保存するように階層を指示しますが、IDE は、それらの項目を保存するために必要なアクションを制御しません。 代わりに、プロジェクトが制御されます。

 ユーザーがエディターで項目を開くと、その項目を制御する階層が選択され、アクティブな階層になります。 選択した階層によって、アイテムに対して実行できるコマンドのセットが決まります。 この方法でユーザー フォーカスを追跡すると、階層にユーザーの現在のコンテキストを反映させることができます。

## <a name="see-also"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
