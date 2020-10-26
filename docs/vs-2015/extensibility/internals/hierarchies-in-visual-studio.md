---
title: 階層
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 22943d3049ff0e24d00c7c29750e7dcd0efaf846
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158362"
---
# <a name="hierarchies-in-visual-studio"></a>Visual Studio での階層
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE: integrated development environment) では、プロジェクトが*階層*として表示されます。 IDE では、階層はノードのツリーで、各ノードには関連付けられたプロパティのセットがあります。 *プロジェクト階層*は、プロジェクトの項目、項目のリレーションシップ、および項目に関連付けられているプロパティとコマンドを保持するコンテナーです。

 では、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 階層インターフェイスを使用してプロジェクト階層を管理し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。 インターフェイスは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> プロジェクト項目から呼び出したコマンドを、標準コマンドハンドラーではなく、適切な階層ウィンドウにリダイレクトします。

## <a name="project-hierarchies"></a>プロジェクト階層
 各プロジェクト階層には、表示および編集できるアイテムが含まれています。 これらの項目は、プロジェクトの種類によって異なります。 たとえば、データベースプロジェクトには、ストアドプロシージャ、データベースビュー、およびデータベーステーブルが含まれる場合があります。 一方、プログラミング言語プロジェクトには、ビットマップおよびダイアログボックスのソースファイルとリソースファイルが含まれていることがあります。 階層を入れ子にすることができます。これにより、プロジェクト階層を作成するときに柔軟性を高めることができます。

 新しいプロジェクトの種類を作成すると、プロジェクトの種類によって、編集可能な項目の完全なセットが制御されます。 ただし、プロジェクトには、編集がサポートされていない項目を含めることができます。 たとえば、Visual C++ に html ファイルの種類のカスタマイズされたエディターが用意されていない場合でも、Visual C++ プロジェクトに HTML ファイルを含めることができます。

 階層は、含まれているアイテムの永続性を管理します。 階層の実装では、階層内のアイテムの永続性に影響する特別なプロパティを制御する必要があります。 たとえば、アイテムがファイルではなくリポジトリ内のオブジェクトを表す場合、階層の実装では、それらのオブジェクトの永続性を制御する必要があります。 IDE 自体は、ユーザー入力に準拠して項目を保存するように階層に指示しますが、IDE はこれらの項目を保存するために必要な操作を制御しません。 代わりに、プロジェクトは制御されています。

 ユーザーがエディターで項目を開くと、その項目を制御する階層が選択され、アクティブな階層になります。 選択した階層によって、その項目に対して操作できるコマンドのセットが決まります。 この方法でユーザーフォーカスを追跡することで、階層にユーザーの現在のコンテキストを反映させることができます。

## <a name="see-also"></a>参照
 IDE の[プロジェクトの種類](../../extensibility/internals/project-types.md)の[選択と通貨 IDE の](../../extensibility/internals/selection-and-currency-in-the-ide.md) [vssdk サンプル](../../misc/vssdk-samples.md)
