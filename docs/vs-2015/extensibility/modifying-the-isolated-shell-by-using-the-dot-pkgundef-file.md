---
title: を使用して、分離シェルを変更します。Pkgundef File |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .pkgundef file
ms.assetid: 9cee2a20-f8ac-4d9d-aef9-068fcd9f27a4
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eab02fe900e96ba37c63faae535974788f99ba78
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538392"
---
# <a name="modifying-the-isolated-shell-by-using-the-pkgundef-file"></a>.Pkgundef ファイルを使用した分離シェルの変更
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Pkgundef ファイルを変更して、指定したレジストリエントリを分離シェルアプリケーションから除外することができます。 通常、コンピューターでアプリケーションを初めて起動すると、Visual Studio シェルによって、既存の Visual Studio レジストリエントリがアプリケーションのルートレジストリキーにコピーされます。 これには、現在インストールされている Vspackage への参照が含まれます。  
  
 分離シェルアプリケーションから特定のレジストリエントリを除外するには、をアプリケーションに追加します。 pkgundef は、パッケージキーの後にエントリを追加します。 キーとエントリは、pkgdef ファイルと同じように表現されます。つまり、[$RootKey $] または [$RootKey $ \\ *subkey*] and "*entry*" =*value*のようになります。ここで、*サブキー*は、影響を与えるサブキー、 *entry*は削除するエントリ、 *value*はまたはのいずれか `""` `dword:00000000` です。  
  
 レジストリキーから複数のエントリを除外するには、キーを1回だけリストし、除外する各エントリの行を続けます。  
  
 分離シェルアプリケーションからレジストリキー全体を除外するには、アプリケーションにキーを追加します。 pkgundef file は、そのキーのレジストリエントリを指定しません。  
  
 Pkgundef ファイルにコメントを追加できます。 1行のコメントには、最初の2文字として2つのスラッシュを含める必要があります。  
  
 たとえば、[**ツール**] メニューの [**データベースへの接続**] および [**サービスへの接続**] コマンドを削除するには、次の行のコメントを解除します。  
  
```  
[$RootKey$\Packages\{8D8529D3-625D-4496-8354-3DAD630ECC1B}]  
```  
  
 次の行を追加します。  
  
```  
[$RootKey$\Packages\{198E76C1-34C0-424D-9957-B3EBD80265FB}]  
```  
  
 アプリケーションの pkgundef ファイルに適用します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio の機能のパッケージ Guid](../extensibility/package-guids-of-visual-studio-features.md)   
 [分離シェルのカスタマイズ](../extensibility/customizing-the-isolated-shell.md)
