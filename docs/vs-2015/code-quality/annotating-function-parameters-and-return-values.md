---
title: 関数のパラメーターと戻り値に注釈を付ける |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- _Outptr_opt_result_bytebuffer_to_
- _Inout_updates_all_opt_
- _Post_equal_to_
- _Outptr_opt_result_maybenull_
- _Out_writes_bytes_all_
- _Out_writes_all_opt_
- _In_opt_
- _Outptr_
- _Outptr_result_maybenull_
- _Outref_result_bytebuffer_all_maybenull_
- _Inout_updates_opt_z_
- _Inout_updates_z_
- _Out_writes_
- _Out_writes_to_ptr_opt_z_
- _In_reads_to_ptr_opt_
- _Ret_writes_to_maybenull_
- _Outref_result_maybenull_
- _Ret_writes_bytes_
- _Outptr_result_bytebuffer_
- _Out_writes_opt_
- _Inout_updates_bytes_opt_
- _In_z_
- _Inout_updates_to_
- _Ret_maybenull_
- _Ret_writes_bytes_to_
- _Ret_z_
- _COM_Outptr_
- _Ret_maybenull_z_
- _Out_opt_
- _In_reads_opt_z_
- _Outptr_result_bytebuffer_to_
- _Ret_notnull_
- _COM_Outptr_opt_result_maybenull_
- _Inout_updates_to_opt_
- _Inout_updates_
- _Outptr_opt_result_buffer_
- _Outptr_result_buffer_to_
- _Out_writes_to_ptr_opt_
- _Out_writes_bytes_all_opt_
- _Inout_updates_all_
- _Deref_inout_range_
- _Ret_writes_
- _Out_writes_z_
- _Ret_writes_to_
- _Out_writes_to_ptr_z_
- _Out_writes_bytes_to_opt_
- _In_reads_or_z_
- _Inout_updates_bytes_to_
- _In_reads_z_
- _In_opt_z_
- _Outref_result_buffer_maybenull_
- _Ret_range_
- _COM_Outptr_opt_
- _Ouptr_opt_result_maybenull_z_
- _In_reads_opt_
- _Inout_
- _Field_range_
- _Ret_writes_z_
- _Out_writes_to_
- _Out_writes_to_ptr_
- _Inout_opt_z_
- _Outref_
- _Deref_out_range_
- _Outref_result_buffer_
- _Outref_result_buffer_to_
- _Outref_result_bytebuffer_to_maybenull_
- _In_reads_bytes_
- _Outptr_opt_result_buffer_to_
- _Outref_result_buffer_all_
- _Out_writes_bytes_to_
- _Result_zeroonfailure_
- _In_reads_bytes_opt_
- _Outref_result_buffer_to_maybenull_
- _Outref_result_bytebuffer_all_
- _Outref_result_buffer_all_maybenull_
- _Ret_writes_maybenull_z_
- _In_range_
- _Inout_updates_bytes_all_opt_
- _Outref_result_bytebuffer_to_
- _Inout_updates_bytes_to_opt_
- _Pre_equal_to_
- _Ret_writes_bytes_maybenull_
- _COM_Outptr_result_maybenull_
- _Ret_writes_maybenull_
- _Out_writes_bytes_
- _Outptr_opt_
- _Out_writes_opt_z_
- _Outref_result_nullonfailure_
- _Outptr_opt_result_z_
- _Inout_opt_
- _Deref_in_range_
- _Outptr_result_z_
- _In_reads_to_ptr_opt_z_
- _Struct_size_bytes_
- _Outptr_result_nullonfailure_
- _In_
- _Inout_updates_bytes_
- _In_reads_to_ptr_z_
- _Ret_writes_bytes_to_maybenull
- _Outptr_opt_result_nullonfailure_
- _In_reads_to_ptr_
- _Outptr_result_buffer_
- _Out_
- _Outref_result_bytebuffer_maybenull_
- _Outptr_result_maybenull_z_
- _In_reads_
- _Inout_updates_opt_
- _Out_writes_to_opt_
- _Outptr_opt_result_bytebuffer_
- _Out_writes_all_
- _Out_range_
- _Inout_updates_bytes_all_
- _Inout_z_
- _Outref_result_bytebuffer_
- _Result_nullonfailure_
- _Ret_null_
ms.assetid: 82826a3d-0c81-421c-8ffe-4072555dca3a
caps.latest.revision: 17
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 71854388f3fb1c5eaea7d40ed2757af9cecacf1a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543807"
---
# <a name="annotating-function-parameters-and-return-values"></a>関数パラメーターおよび戻り値の注釈設定
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この記事では、単純な関数パラメーター (スカラー、構造体とクラスへのポインター)、およびほとんどの種類のバッファーに対する注釈の一般的な使用方法について説明します。  この記事では、注釈の一般的な使用パターンについても説明します。 関数に関連するその他の注釈については、「[関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)」を参照してください。  
  
## <a name="pointer-parameters"></a>ポインター パラメーター  
 次の表の注釈については、ポインターパラメーターに注釈を付けると、ポインターが null の場合、アナライザーはエラーを報告します。  これは、ポインターと、ポイントされている任意のデータ項目に適用されます。  
  
 **注釈と説明**  
  
- `_In_`  
  
     スカラー、構造体、構造体へのポインター、およびなどの入力パラメーターに注釈を入力します。  単純なスカラーでは、明示的に使用できます。  パラメーターは、事前状態で有効である必要があり、変更されません。  
  
- `_Out_`  
  
     スカラー、構造体、構造体へのポインター、およびなどの出力パラメーターに注釈を記述します。  値で渡されるスカラーなど、値を返すことができないオブジェクトには適用しないでください。  パラメーターは、事前状態では有効である必要はありませんが、事後状態で有効である必要があります。  
  
- `_Inout_`  
  
     関数によって変更されるパラメーターに注釈を設定します。  これは、事前状態と事後状態の両方で有効である必要がありますが、呼び出しの前後に異なる値があると見なされます。 変更可能な値に適用する必要があります。  
  
- `_In_z_`  
  
     入力として使用される、null で終わる文字列へのポインター。  文字列は、事前状態で有効である必要があります。  には、 `PSTR` 既に正しい注釈があるのバリアントが推奨されています。  
  
- `_Inout_z_`  
  
     変更される null で終わる文字配列へのポインター。  呼び出しの前後で有効である必要がありますが、値は変更されたと見なされます。  Null 終端文字は移動できますが、元の null 終端文字までの要素のみがアクセスされる可能性があります。  
  
- `_In_reads_(s)`  
  
     `_In_reads_bytes_(s)`  
  
     関数によって読み取られる配列へのポインター。  配列はサイズの `s` 要素であり、すべて有効である必要があります。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_In_reads_z_(s)`  
  
     Null で終了し、既知のサイズを持つ配列へのポインター。 Null 終端文字までの要素 ( `s` null 終端文字がない場合) は、事前状態で有効である必要があります。  サイズがバイト単位でわかっている場合は、 `s` 要素のサイズでスケールします。  
  
- `_In_reads_or_z_(s)`  
  
     Null で終わるか、既知のサイズ (またはその両方) を持つ配列へのポインター。 Null 終端文字までの要素 ( `s` null 終端文字がない場合) は、事前状態で有効である必要があります。  サイズがバイト単位でわかっている場合は、 `s` 要素のサイズでスケールします。  (ファミリで使用され `strn` ます)。  
  
- `_Out_writes_(s)`  
  
     `_Out_writes_bytes_(s)`  
  
     `s`関数によって書き込まれる要素の配列 (resp) へのポインター。  配列要素は、事前状態で有効である必要はなく、事後状態で有効な要素の数が指定されていません。  パラメーターの型に注釈がある場合は、事後状態で適用されます。 次に例を示します。  
  
     `typedef _Null_terminated_ wchar_t *PWSTR; void MyStringCopy(_Out_writes_ (size) PWSTR p1,    _In_ size_t size,    _In_ PWSTR p2);`  
  
     この例では、呼び出し元はの要素のバッファーを提供し `size` `p1` ます。  `MyStringCopy`これらの要素の一部を有効にします。 さらに重要なの `_Null_terminated_` は、の注釈は、 `PWSTR` `p1` が post 状態で null で終了することを意味します。  この方法では、有効な要素の数は引き続き明確に定義されますが、特定の要素数は必要ありません。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_Out_writes_z_(s)`  
  
     要素の配列へのポインター `s` 。  要素は、事前状態で有効である必要はありません。  事後の状態では、null 終端文字 (存在する必要がある) を介して要素が有効である必要があります。  サイズがバイト単位でわかっている場合は、 `s` 要素のサイズでスケールします。  
  
- `_Inout_updates_(s)`  
  
     `_Inout_updates_bytes_(s)`  
  
     配列へのポインター。関数内で読み取りと書き込みの両方を行います。  これはサイズの要素であり、 `s` 事前状態と事後状態で有効です。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_Inout_updates_z_(s)`  
  
     Null で終了し、既知のサイズを持つ配列へのポインター。 Null 終端文字 (存在する必要がある) までの要素は、事前状態と事後状態の両方で有効である必要があります。  事後状態の値は、前の状態の値とは異なるものと見なされます。これには、null 終端文字の場所も含まれます。 サイズがバイト単位でわかっている場合は、 `s` 要素のサイズでスケールします。  
  
- `_Out_writes_to_(s,c)`  
  
     `_Out_writes_bytes_to_(s,c)`  
  
     `_Out_writes_all_(s)`  
  
     `_Out_writes_bytes_all_(s)`  
  
     要素の配列へのポインター `s` 。  要素は、事前状態で有効である必要はありません。  事後の状態では、 `c` -th 要素までの要素が有効である必要があります。  サイズがバイト単位でわかっている場合は、スケール `s` と `c` 要素サイズを使用するか、次のように定義されている `_bytes_` variant を使用します。  
  
     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`  
  
     つまり、前の状態にあるバッファーに存在するすべての要素 `s` は、post 状態で有効です。  次に例を示します。  
  
     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`  
  
- `_Inout_updates_to_(s,c)`  
  
     `_Inout_updates_bytes_to_(s,c)`  
  
     配列へのポインター。この配列は、関数によって読み取られ、書き込まれます。  これはサイズの `s` 要素であり、すべてが事前状態で有効である必要があり、 `c` 要素は事後状態で有効である必要があります。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_Inout_updates_z_(s)`  
  
     Null で終了し、既知のサイズを持つ配列へのポインター。 Null 終端文字 (存在する必要がある) までの要素は、事前状態と事後状態の両方で有効である必要があります。  事後状態の値は、前の状態の値とは異なるものと見なされます。これには、null 終端文字の場所も含まれます。 サイズがバイト単位でわかっている場合は、 `s` 要素のサイズでスケールします。  
  
- `_Out_writes_to_(s,c)`  
  
     `_Out_writes_bytes_to_(s,c)`  
  
     `_Out_writes_all_(s)`  
  
     `_Out_writes_bytes_all_(s)`  
  
     要素の配列へのポインター `s` 。  要素は、事前状態で有効である必要はありません。  事後の状態では、 `c` -th 要素までの要素が有効である必要があります。  サイズがバイト単位でわかっている場合は、スケール `s` と `c` 要素サイズを使用するか、次のように定義されている `_bytes_` variant を使用します。  
  
     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`  
  
     つまり、前の状態にあるバッファーに存在するすべての要素 `s` は、post 状態で有効です。  次に例を示します。  
  
     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`  
  
- `_Inout_updates_to_(s,c)`  
  
     `_Inout_updates_bytes_to_(s,c)`  
  
     配列へのポインター。この配列は、関数によって読み取られ、書き込まれます。  これはサイズの `s` 要素であり、すべてが事前状態で有効である必要があり、 `c` 要素は事後状態で有効である必要があります。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_Inout_updates_all_(s)`  
  
     `_Inout_updates_bytes_all_(s)`  
  
     サイズ要素の関数によって読み取られ、書き込まれる配列へのポインター `s` 。 次の同等のものとして定義されます。  
  
     `_Inout_updates_to_(_Old_(s), _Old_(s))    _Inout_updates_bytes_to_(_Old_(s), _Old_(s))`  
  
     つまり、前の状態にあるバッファーに存在するすべての要素 `s` は、事前状態と事後状態で有効です。  
  
     バリアントは、 `_bytes_` 要素の代わりにサイズをバイト単位で示します。 この値は、サイズを要素として表現できない場合にのみ使用してください。  たとえば、文字列では、を `char` `_bytes_` 使用する同様の関数がの場合にのみ、バリアントが使用さ `wchar_t` れます。  
  
- `_In_reads_to_ptr_(p)`  
  
     式 `p` `_Curr_` (つまり、から `p` マイナス `_Curr_` ) が適切な言語標準によって定義されている配列へのポインター。  の前の要素は、 `p` 事前状態で有効である必要があります。  
  
- `_In_reads_to_ptr_z_(p)`  
  
     Null で終わる配列へのポインター `p` `_Curr_` 。式 (つまり、からの `p` 減算 `_Curr_` ) は、適切な言語標準によって定義されます。  の前の要素は、 `p` 事前状態で有効である必要があります。  
  
- `_Out_writes_to_ptr_(p)`  
  
     式 `p` `_Curr_` (つまり、から `p` マイナス `_Curr_` ) が適切な言語標準によって定義されている配列へのポインター。  より前の要素は、 `p` 事前状態で有効である必要はなく、事後状態で有効である必要があります。  
  
- `_Out_writes_to_ptr_z_(p)`  
  
     Null で終わる配列へのポインター `p` `_Curr_` 。式 (つまり、からの `p` 減算 `_Curr_` ) は、適切な言語標準によって定義されます。  より前の要素は、 `p` 事前状態で有効である必要はなく、事後状態で有効である必要があります。  
  
## <a name="optional-pointer-parameters"></a>省略可能なポインター パラメーター  
 ポインターパラメーター注釈にが含まれている場合は、 `_opt_` パラメーターが null である可能性があることを示します。 それ以外の場合、注釈はを含まないバージョンと同じように実行され `_opt_` ます。 `_opt_`ポインターパラメーター注釈のバリアントの一覧を次に示します。  
  
`_In_opt_`, `_Out_opt_`, `_Inout_opt_`, `_In_opt_z_`, `_Inout_opt_z_`, `_In_reads_opt_`, `_In_reads_bytes_opt_`, `_In_reads_opt_z_`|`_Out_writes_opt_`, `_Out_writes_opt_z_`, `_Inout_updates_opt_`, `_Inout_updates_bytes_opt_`, `_Inout_updates_opt_z_`, `_Out_writes_to_opt_`, `_Out_writes_bytes_to_opt_`, `_Out_writes_all_opt_`, `_Out_writes_bytes_all_opt_`|`_Inout_updates_to_opt_`, `_Inout_updates_bytes_to_opt_`, `_Inout_updates_all_opt_`, `_Inout_updates_bytes_all_opt_`, `_In_reads_to_ptr_opt_`, `_In_reads_to_ptr_opt_z_`, `_Out_writes_to_ptr_opt_`, `_Out_writes_to_ptr_opt_z_`|  
  
## <a name="output-pointer-parameters"></a>出力のポインター パラメーター  
 出力ポインターパラメーターは、パラメーターとポイント先の位置を明確に区別するために特別な表記を必要とします。  
  
 **注釈と説明**  
  
- `_Outptr_`  
  
   パラメーターを null にすることはできません。また、post 状態では、ポイント先の場所を null にすることはできず、有効である必要があります。  
  
- `_Outptr_opt_`  
  
   パラメーターは null でもかまいませんが、post 状態では、ポイント先の場所を null にすることはできず、有効である必要があります。  
  
- `_Outptr_result_maybenull_`  
  
   パラメーターを null にすることはできません。また、状態を示す位置を null にすることもできます。  
  
- `_Outptr_opt_result_maybenull_`  
  
   パラメーターは null にすることができます。また、状態を示す位置を null にすることもできます。  
  
  次の表では、注釈の意味をさらに修飾するために、注釈名に追加の部分文字列が挿入されています。  さまざまな部分文字列は、、、、 `_z` `_COM_` `_buffer_` `_bytebuffer_` 、および `_to_` です。  
  
> [!IMPORTANT]
> 注釈を付けているインターフェイスが COM である場合は、これらの注釈の COM 形式を使用します。 COM 注釈は、他の型インターフェイスと一緒に使用しないでください。  
  
 **注釈と説明**  
  
- `_Outptr_result_z_`  
  
   `_Outptr_opt_result_z_`  
  
   `_Outptr_result_maybenull_z_`  
  
   `_Ouptr_opt_result_maybenull_z_`  
  
   返されたポインターには注釈があり `_Null_terminated_` ます。  
  
- `_COM_Outptr_`  
  
   `_COM_Outptr_opt_`  
  
   `_COM_Outptr_result_maybenull_`  
  
   `_COM_Outptr_opt_result_maybenull_`  
  
   返されたポインターには COM セマンティクスがあるため、 `_On_failure_` 返されたポインターが null であることを示す事後条件が発生します。  
  
- `_Outptr_result_buffer_(s)`  
  
   `_Outptr_result_bytebuffer_(s)`  
  
   `_Outptr_opt_result_buffer_(s)`  
  
   `_Outptr_opt_result_bytebuffer_(s)`  
  
   返されたポインターは、サイズ要素またはバイトの有効なバッファーを指して `s` います。  
  
- `_Outptr_result_buffer_to_(s, c)`  
  
   `_Outptr_result_bytebuffer_to_(s, c)`  
  
   `_Outptr_opt_result_buffer_to_(s,c)`  
  
   `_Outptr_opt_result_bytebuffer_to_(s,c)`  
  
   返されたポインターは、 `s` 1 つ目が有効なサイズ要素またはバイトのバッファーを指して `c` います。  
  
  特定のインターフェイスの規則では、出力パラメーターが失敗時に nullified されることを前提としています。  明示的な COM コードを除き、次の表のフォームを使用することをお勧めします。  COM コードの場合は、前のセクションで示した対応する COM フォームを使用します。  
  
  **注釈と説明**  
  
- `_Result_nullonfailure_`  
  
   他の注釈を変更します。 関数が失敗した場合、結果は null に設定されます。  
  
- `_Result_zeroonfailure_`  
  
   他の注釈を変更します。 関数が失敗した場合、結果は0に設定されます。  
  
- `_Outptr_result_nullonfailure_`  
  
   関数が成功した場合、返されるポインターは有効なバッファーを指します。関数が失敗した場合は null を指します。 この注釈は、省略可能なパラメーターに対してのみ使用されます。  
  
- `_Outptr_opt_result_nullonfailure_`  
  
   関数が成功した場合、返されるポインターは有効なバッファーを指します。関数が失敗した場合は null を指します。 この注釈は省略可能なパラメーターのためのものです。  
  
- `_Outref_result_nullonfailure_`  
  
   関数が成功した場合、返されるポインターは有効なバッファーを指します。関数が失敗した場合は null を指します。 この注釈は、参照パラメーターを対象としています。  
  
## <a name="output-reference-parameters"></a>出力の参照パラメーター  
 参照パラメーターの一般的な使用方法は、出力パラメーター用です。  単純な出力参照パラメーター (など) の場合、 `int&` `_Out_` は正しいセマンティクスを提供します。  ただし、出力値がポインターの場合 (たとえば)、の `int *&` ような同等のポインター注釈は、 `_Outptr_ int **` 正しいセマンティクスを提供しません。  ポインター型の出力参照パラメーターのセマンティクスを簡潔に表現するには、次の複合注釈を使用します。  
  
 **注釈と説明**  
  
- `_Outref_`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。  
  
- `_Outref_result_maybenull_`  
  
     結果は事後状態で有効である必要がありますが、事後状態では null である可能性があります。  
  
- `_Outref_result_buffer_(s)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 は、サイズ要素の有効なバッファーを指し `s` ます。  
  
- `_Outref_result_bytebuffer_(s)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 サイズバイトの有効なバッファーを指して `s` います。  
  
- `_Outref_result_buffer_to_(s, c)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 は、要素のバッファーを指し `s` ます。最初の要素は `c` 有効です。  
  
- `_Outref_result_bytebuffer_to_(s, c)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 `s`最初のが有効なバイトのバッファーを指し `c` ます。  
  
- `_Outref_result_buffer_all_(s)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 有効なバッファーサイズの有効な要素を指して `s` います。  
  
- `_Outref_result_bytebuffer_all_(s)`  
  
     結果は、事後の状態で有効である必要があります。 null にすることはできません。 有効な要素のバイトの有効なバッファーを指して `s` います。  
  
- `_Outref_result_buffer_maybenull_(s)`  
  
     結果は事後状態で有効である必要がありますが、事後状態では null である可能性があります。 は、サイズ要素の有効なバッファーを指し `s` ます。  
  
- `_Outref_result_bytebuffer_maybenull_(s)`  
  
     結果は事後状態で有効である必要がありますが、事後状態では null である可能性があります。 サイズバイトの有効なバッファーを指して `s` います。  
  
- `_Outref_result_buffer_to_maybenull_(s, c)`  
  
     結果は事後状態で有効である必要がありますが、事後状態では null である可能性があります。 は、要素のバッファーを指し `s` ます。最初の要素は `c` 有効です。  
  
- `_Outref_result_bytebuffer_to_maybenull_(s,c)`  
  
     結果は事後状態で有効である必要がありますが、post 状態では null である可能性があります。 `s`最初のが有効なバイトのバッファーを指し `c` ます。  
  
- `_Outref_result_buffer_all_maybenull_(s)`  
  
     結果は事後状態で有効である必要がありますが、post 状態では null である可能性があります。 有効なバッファーサイズの有効な要素を指して `s` います。  
  
- `_Outref_result_bytebuffer_all_maybenull_(s)`  
  
     結果は事後状態で有効である必要がありますが、post 状態では null である可能性があります。 有効な要素のバイトの有効なバッファーを指して `s` います。  
  
## <a name="return-values"></a>戻り値  
 関数の戻り値はパラメーターに似てい `_Out_` ますが、逆参照のレベルが異なるため、結果へのポインターの概念を考慮する必要はありません。  次の注釈について、戻り値は注釈付きオブジェクト (スカラー、構造体へのポインター、またはバッファーへのポインター) です。 これらの注釈は、対応する注釈と同じセマンティクスを持ち `_Out_` ます。  
  
`_Ret_z_`, `_Ret_writes_(s)`, `_Ret_writes_bytes_(s)`, `_Ret_writes_z_(s)`, `_Ret_writes_to_(s,c)`, `_Ret_writes_maybenull_(s)`, `_Ret_writes_to_maybenull_(s)`, `_Ret_writes_maybenull_z_(s)`|`_Ret_maybenull_`, `_Ret_maybenull_z_`, `_Ret_null_`, `_Ret_notnull_`, `_Ret_writes_bytes_to_`, `_Ret_writes_bytes_maybenull_`, `_Ret_writes_bytes_to_maybenull_`
  
## <a name="other-common-annotations"></a>その他の一般的な注釈  
 **注釈と説明**  
  
- `_In_range_(low, hi)`  
  
     `_Out_range_(low, hi)`  
  
     `_Ret_range_(low, hi)`  
  
     `_Deref_in_range_(low, hi)`  
  
     `_Deref_out_range_(low, hi)`  
  
     `_Deref_inout_range_(low, hi)`  
  
     `_Field_range_(low, hi)`  
  
     パラメーター、フィールド、または結果は、からまでの範囲内に `low` あります (を含む) `hi` 。  `_Satisfies_(_Curr_ >= low && _Curr_ <= hi)`注釈付きオブジェクトに適切な状態または状態の条件と共に適用されると同じです。  
  
    > [!IMPORTANT]
    > 名前には "in" と "out" が含まれていますが、とのセマンティクスは `_In_` `_Out_` これらの注釈には適用**されません**。  
  
- `_Pre_equal_to_(expr)`  
  
     `_Post_equal_to_(expr)`  
  
     注釈付きの値は正確に `expr` です。  `_Satisfies_(_Curr_ == expr)`注釈付きオブジェクトに適切な状態または状態の条件と共に適用されると同じです。  
  
- `_Struct_size_bytes_(size)`  
  
     構造体またはクラスの宣言に適用されます。  この型の有効なオブジェクトが、で指定されたバイト数を使用して、宣言された型よりも大きくなる可能性があることを示し `size` ます。  次に例を示します。  
  
     `typedef _Struct_size_bytes_(nSize) struct MyStruct {    size_t nSize;    ... };`  
  
     次に、型のパラメーターのバッファーサイズ (バイト単位) を `pM` `MyStruct *` 次のように取得します。  
  
     `min(pM->nSize, sizeof(MyStruct))`  
  
## <a name="related-resources"></a>関連リソース  
 [コード分析チームのブログ](https://blogs.msdn.com/b/codeanalysis/)  
  
## <a name="see-also"></a>関連項目  
 [SAL 注釈を使用して C/c + + コードの欠陥を減らす](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)   
 [SAL について](../code-quality/understanding-sal.md)   
 [関数の動作に注釈を付ける](../code-quality/annotating-function-behavior.md)   
 [構造体とクラスに注釈を付ける](../code-quality/annotating-structs-and-classes.md)   
 [ロック動作に注釈を付ける](../code-quality/annotating-locking-behavior.md)   
 [注釈を適用するタイミングと場所の指定](../code-quality/specifying-when-and-where-an-annotation-applies.md)   
 [組み込み関数](../code-quality/intrinsic-functions.md)   
 [ベスト プラクティスと例](../code-quality/best-practices-and-examples-sal.md)
