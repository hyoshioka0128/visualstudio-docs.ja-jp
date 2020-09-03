---
title: SccGetEvents 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetEvents
helpviewer_keywords:
- SccGetEvents function
ms.assetid: 32f8147d-6dcc-465e-b07b-42da5824f9b0
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d975570334aeab7c6709db92f3240a8e8d06b131
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200113"
---
# <a name="sccgetevents-function"></a>SccGetEvents 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、キューに置かれた状態イベントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccGetEvents (  
   LPVOID pvContext,  
   LPSTR  lpFileName,  
   LPLONG lpStatus,  
   LPLONG pnEventsRemaining  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pvContext  
 からソース管理プラグインのコンテキスト構造。  
  
 lpFileName  
 [入力、出力]ソース管理プラグインが、返されたファイル名 (最大 _MAX_PATH 文字) を配置するバッファー。  
  
 lpStatus  
 [入力、出力]ステータスコードを返します (有効な値については、 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md) を参照してください)。  
  
 pnEventsRemaining  
 [入力、出力]この呼び出しの後にキューに残されたエントリの数を返します。 この数値が大きい場合、呼び出し元は [Sccqueryinfo](../extensibility/sccqueryinfo-function.md) を呼び出して、すべての情報を一度に取得することができます。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|イベントの取得に成功しました。|  
|SCC_E_OPNOTSUPPORTED|この関数はサポートされません。|  
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|  
  
## <a name="remarks"></a>注釈  
 この関数は、アイドル処理中に呼び出され、ソース管理下にあるファイルのステータスの更新があるかどうかを確認します。 ソース管理プラグインは、認識しているすべてのファイルの状態を保持し、プラグインによって状態の変更が通知されるたびに、状態と関連付けられたファイルがキューに格納されます。 `SccGetEvents`が呼び出されると、キューの最上位要素が取得され、返されます。 この関数は、以前にキャッシュされた情報のみを返すように制限されており、非常に迅速なターンアラウンドが必要です (つまり、ディスクの読み取りや、ソース管理システムの状態の確認を行う必要はありません)。そうしないと、IDE のパフォーマンスが低下することがあります。  
  
 レポートするステータスの更新がない場合、ソース管理プラグインはが指すバッファーに空の文字列を格納し `lpFileName` ます。 それ以外の場合、プラグインは、ステータス情報が変更されたファイルの完全なパス名を格納し、適切な状態コード ([ [ファイルステータスコード](../extensibility/file-status-code-enumerator.md)] で詳細に説明されている値の1つ) を返します。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
