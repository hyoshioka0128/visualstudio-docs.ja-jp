---
title: Visual Studio での階層 |Microsoft Docs
description: 'プロジェクト項目とそれらに関連付けられたプロパティを含む、Visual Studio 統合開発環境 (IDE: integrated development environment) のプロジェクト階層について説明します。'
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 5a7126f52517b1028cf878750294f1d4c7dbfe26
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480357"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio での階層
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE: integrated development environment) では、プロジェクトが *階層* として表示されます。 IDE では、階層はノードのツリーで、各ノードには関連付けられたプロパティのセットがあります。 *プロジェクト階層* は、プロジェクトの項目、項目のリレーションシップ、および項目に関連付けられているプロパティとコマンドを保持するコンテナーです。

 では、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 階層インターフェイスを使用してプロジェクト階層を管理し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> プロジェクト項目から呼び出したコマンドを、標準コマンドハンドラーではなく、適切な階層ウィンドウにリダイレクトします。

## <a name="project-hierarchies"></a>プロジェクト階層
 各プロジェクト階層には、表示および編集できるアイテムが含まれています。 これらの項目は、プロジェクトの種類によって異なります。 たとえば、データベースプロジェクトには、ストアドプロシージャ、データベースビュー、およびデータベーステーブルが含まれる場合があります。 一方、プログラミング言語プロジェクトには、ビットマップおよびダイアログボックスのソースファイルとリソースファイルが含まれていることがあります。 階層を入れ子にすることができます。これにより、プロジェクト階層を作成するときに柔軟性を高めることができます。

 新しいプロジェクトの種類を作成すると、プロジェクトの種類によって、編集可能な項目の完全なセットが制御されます。 ただし、プロジェクトには、編集がサポートされていない項目を含めることができます。 たとえば、Visual C++ に html ファイルの種類のカスタマイズされたエディターが用意されていない場合でも、Visual C++ プロジェクトに HTML ファイルを含めることができます。

 階層は、含まれているアイテムの永続性を管理します。 階層の実装では、階層内のアイテムの永続性に影響する特別なプロパティを制御する必要があります。 たとえば、アイテムがファイルではなくリポジトリ内のオブジェクトを表す場合、階層の実装では、それらのオブジェクトの永続性を制御する必要があります。 IDE 自体は、ユーザー入力に準拠して項目を保存するように階層に指示しますが、IDE はこれらの項目を保存するために必要な操作を制御しません。 代わりに、プロジェクトは制御されています。

 ユーザーがエディターで項目を開くと、その項目を制御する階層が選択され、アクティブな階層になります。 選択した階層によって、その項目に対して操作できるコマンドのセットが決まります。 この方法でユーザーフォーカスを追跡することで、階層にユーザーの現在のコンテキストを反映させることができます。

## <a name="see-also"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
