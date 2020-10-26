---
title: ソース管理を実装するかどうかを判断する VSPackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cff53700dcd6a80f841108d5a2b486dcb0ba7a11
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196793"
---
# <a name="determining-whether-to-implement-a-source-control-vspackage"></a>ソース管理 VSPackage を実装するかどうかの決定
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このセクションでは、ソース管理ソリューションを拡張するためのソース管理プラグインとソース管理 Vspackage の選択について説明し、適切な統合パスの選択に関する幅広いガイドラインを詳述します。  
  
## <a name="small-source-control-solution-with-limited-resources"></a>リソースが限られた小規模なソース管理ソリューション  
 リソースが限られていて、ソース管理パッケージの作成に伴うオーバーヘッドが発生しない場合は、ソース管理プラグイン API ベースのプラグインを作成できます。これにより、ソース管理パッケージと並行して作業を行うことができ、ソース管理プラグインとパッケージを必要に応じて切り替えることができます。 詳細については、「 [登録と選択](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)」を参照してください。  
  
## <a name="large-source-control-solution-with-a-rich-feature-set"></a>豊富な機能セットを備えた大規模なソース管理ソリューション  
 ソース管理プラグイン API を使用して適切にキャプチャされていない、豊富なソース管理モデルを提供するソース管理ソリューションを実装する場合は、統合パスとしてソース管理パッケージを使用することを検討してください。 これは特に、ソース管理アダプターパッケージ (ソース管理プラグインと通信する) を独自のものに置き換えて、ソース管理イベントをカスタムで処理できるようにする場合に特に適用されます。 必要なソース管理 UI が既にあり、そのエクスペリエンスをで保持する場合は、[ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ソース管理パッケージ] オプションを使用すると、その操作を行うことができます。 ソース管理パッケージは汎用ではなく、IDE で使用するためだけに設計されてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 ソース管理のロジックと UI を柔軟かつ高度に制御できるソース管理ソリューションを実装する場合は、ソース管理パッケージの統合ルートを使用することをお勧めします。 次の操作を行います。  
  
1. 独自のソース管理 VSPackage を登録します (「 [登録と選択」を](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)参照してください)。  
  
2. 既定のソース管理 UI をカスタム UI に置き換えます (「 [カスタムユーザーインターフェイス](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)」を参照してください)。  
  
3. 使用するグリフを指定しソリューションエクスプローラーグリフイベントを処理します (「 [グリフコントロール](../../extensibility/internals/glyph-control-source-control-vspackage.md)」を参照してください)。  
  
4. クエリの編集およびクエリの保存イベントを処理します (「 [クエリの編集クエリの保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)」を参照してください)。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
