---
title: CommentMarkAtProfile | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- CommentMarkAtProfile
- CommentMarkAtProfileA
ms.assetid: 04294ca3-bf9c-4c76-86f1-898c2140de27
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 36ebd4a2cd130d63b030e80696dbdde7ff179706
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85531522"
---
# <a name="commentmarkatprofile"></a>CommentMarkAtProfile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`CommentMarkAtProfile` メソッドは、タイムスタンプ値、数字マーク、コメント文字列を .vsp ファイルに挿入します。 タイムスタンプ値は、外部イベントの同期に使用できます。 マークやコメントを挿入するには、CommentMarkAtProfile 関数が含まれるスレッドのプロファイリングをオンにする必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
PROFILE_COMMAND_STATUS PROFILERAPI CommentMarkAtProfile (  
                                   __int64 dnTimestamp,  
                                   long lMarker,  
                                   LPCTSTR szComment);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dnTimestamp`  
  
 タイムスタンプ値を表す 64 ビット整数。  
  
 `lMarker`  
  
 挿入する数字マーカー。 マーカーは 0 以上の値にする必要があります。  
  
 `szComment`  
  
 挿入するテキスト文字列のポインター。 文字列は、NULL 終端文字も含めて 256 文字位内にする必要があります。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 関数の成功または失敗は、**PROFILE_COMMAND_STATUS** 列挙型を使って表されます。 戻り値は次のいずれかになります。  
  
|列挙子|説明|  
|----------------|-----------------|  
|MARK_ERROR_MARKER_RESERVED|パラメーターは 0 以下です。 これらの値は予約済みです。 マークとコメントは記録されません。|  
|MARK_ERROR_MODE_NEVER|関数が呼び出されたときに、プロファイル モードが NEVER に設定されました。 マークとコメントは記録されません。|  
|MARK_ERROR_MODE_OFF|関数が呼び出されたときに、プロファイル モードが OFF に設定されました。 マークとコメントは記録されません。|  
|MARK_ERROR_NO_SUPPORT|このコンテキストでマークがサポートされていません。 マークとコメントは記録されません。|  
|MARK_ERROR_OUTOFMEMORY|メモリ不足のため、このイベントを記録できません。 マークとコメントは記録されません。|  
|MARK_TEXTTOOLONG|文字列の長さが最大値の 256 文字を超えています。 コメント文字列は切り詰められ、マークとコメントが記録されます。|  
|MARK_OK|成功した場合は MARK_OK が返されます。|  
  
## <a name="remarks"></a>Remarks  
 Mark コマンドまたは API 関数 (CommentMarkAtProfile、CommentMarkProfile、または MarkProfile) でマークとコメントが挿入されたとき、マークのプロファイル関数を含むスレッドでは、プロファイル状態をオンにする必要があります。 プロファイル マークは、スコープ内でグローバルです。 たとえば、あるスレッドに挿入したプロファイルマークを、.vsp ファイル内の任意のスレッドで使用し、データ セグメントの開始または終了をマークできます。  
  
> [!IMPORTANT]
> CommentMarkAtProfile メソッドは、インストルメンテーションでのみ使用してください。  
  
## <a name="net-framework-equivalent"></a>同等の .NET Framework 関数  
 Microsoft.VisualStudio.Profiler.dll  
  
## <a name="function-information"></a>関数の情報  
  
|アイテム|[値]|  
|-|-|  
|**Header**|VSPerf.h をインクルードします。|  
|**Library**|VSPerf.lib を使用します。|  
|**Unicode**|CommentMarkAtProfileW (Unicode) と CommentMarkAtProfileA (ANSI) として実装されます。|  
  
## <a name="example"></a>例  
 次のコードは、汎用関数呼び出しの CommentMarkAtProfile の使用を表しています。 この例では、コードで ANSI 対応関数を呼び出すかどうかを判断するために、Win32 文字列マクロおよび ANSI のコンパイラ設定が使用されていることを前提としています。  
  
```  
void ExerciseCommentMarkAtProfile(void)  
{  
    // Declare and initalize variables to pass to   
    // CommentMarkAtProfile.  The values of these   
    // parameters are assigned based on the needs   
    // of the code; and for the sake of simplicity  
    // in this example, the variables are assigned  
    // arbitrary values.  
    int64 timeStamp = 0x1111;  
    long markId = 01;  
    TCHAR * markText = TEXT("Exercising CommentMarkAtProfile...");  
  
    // Variables used to print output.  
    HRESULT hResult;  
    TCHAR tchBuffer[256];  
  
    // Declare MarkOperationResult Enumerator.    
    // Holds return value from call to CommentMarkAtProfile.  
    PROFILE_COMMAND_STATUS markResult;  
  
    markResult = CommentMarkAtProfile(  
        timeStamp,  
        markId,  
        markText);  
  
    // Format and print result.  
    LPCTSTR pszFormat = TEXT("%s %d.\0");  
    TCHAR* pszTxt = TEXT("CommentMarkAtProfile returned");  
    hResult = StringCchPrintf(tchBuffer, 256, pszFormat,   
    pszTxt, markResult);  
  
#ifdef DEBUG  
    OutputDebugString(tchBuffer);  
#endif  
}  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio Profiler API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)
