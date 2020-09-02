---
title: Visual Studio コマンドテーブル (.Vsct) Files |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cde3b86e19788c41df6e8f1c79a6bf829f491170
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675245"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio Command Table (.Vsct) ファイル
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コマンドテーブル構成ファイルは、VSPackage に含まれる一連のコマンドを記述したテキストファイルです。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]コマンドテーブル (vsct) コンパイラは、XML ベースの構成ファイル (vsct ファイル) をバイナリコマンドテーブル出力 (cto) ファイルにコンパイルします。 結果として得られる cto ファイルは、コマンドテーブル (CTC) コンパイラを使用して ctc 構成ファイルをコンパイルすることによって作成されるファイルと同じです。 ただし、xml ベースの vsct ファイルには、XML エディターや XML IntelliSense など、いくつかの利点があります。  
  
 Vsct ファイルの構文とセマンティクスの詳細については、「XML コマンドテーブルの設計」 (「」を参照してください [。Vsct) ファイル](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XML コマンド テーブル (.Vsct) ファイルの設計](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)  
 Vsct ファイルをデザインする方法について説明します。  
  
 [方法: .Vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)  
 Vsct ファイルを作成するためのメソッドを比較します。 新しい vsct ファイルを手動で作成するプロセスについて説明します。  
  
## <a name="related-sections"></a>関連項目  
 [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)  
 コマンドテーブルの XML 構成ファイルの各セクションの詳細について説明します。  
  
 [コマンドテーブルの構成 (を実行します。Ctc) ファイル](https://msdn.microsoft.com/3413dda1-f372-4669-bcf0-c64d3463842c)  
 非推奨の ctc ファイル形式の概要を示します。  
  
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 コマンドテーブル形式の指定について説明します。  
  
 [VSPackage のリソース](../../extensibility/internals/resources-in-vspackages.md)  
 マネージ Vspackage でマネージリソースとアンマネージリソースを使用する方法について説明します。  
  
 [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)  
 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
