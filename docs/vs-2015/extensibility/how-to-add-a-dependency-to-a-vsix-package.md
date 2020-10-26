---
title: '方法: VSIX パッケージに依存関係を追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 997c0df133b72d69dfb4e69de53a1b77e1a0965c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697504"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>方法: VSIX パッケージへの依存関係の追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ターゲットコンピューターにまだ存在しないすべての依存関係をインストールする VSIX パッケージの配置を設定できます。 これを実現するには、VSIX の依存関係を source.extension.vsixmanifest ファイルに追加します。  
  
#### <a name="to-add-a-dependency"></a>依存関係を追加するには  
  
1. **デザイン**ビューで source.extension.vsixmanifest ファイルを開きます。 [ **依存関係** ] タブにアクセスし、[ **新規**] をクリックします。  
  
2. インストールされている拡張機能を追加するには、[ **新しい依存関係の追加** ] ダイアログボックスで [ **インストールされている拡張機能** ] を選択し、[ **名前**] に一覧の拡張子を選択します。  
  
3. インストールされていない別の VSIX を追加するには:: [ **新しい依存関係の追加** ] ダイアログボックスで、[ **ファイルシステム上のファイル** ] を選択し、[ **参照** ] ボタンを使用して vsix を選択します。  
  
## <a name="see-also"></a>参照  
 [VSIX 拡張機能スキーマ1.0 リファレンス](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)   
 [Windows インストーラーの配置に関する拡張機能を準備する](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
