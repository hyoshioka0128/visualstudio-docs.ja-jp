---
title: '方法: 最適化されたコードをデバッグする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- breakpoints, in optimized code
- debugging [C++], optimized code
- optimization, debug builds
- debug builds, optimizing
- optimized code, debugging
ms.assetid: fc8eeeb8-6629-4c9b-99f7-2016aee81dff
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68ce036d420293e8a75bec1b2cac9f9ee8f8fcd2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675610"
---
# <a name="how-to-debug-optimized-code"></a>方法: 最適化されたコードをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

注意]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、[ツール] メニューの [設定のインポートとエクスポート] をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。  
  
> [!NOTE]
> Visual Studio 更新プログラム 3 で導入された [/Zo (最適化されたデバッグ機能の強化)](https://msdn.microsoft.com/library/eea8d89a-7fe0-4fe1-86b2-7689bbebbd7f) コンパイラ オプションを使用すると、最適化されたコードについて豊富なデバッグ情報が生成されます ( **/Od** コンパイラ オプションを使用しないでビルドされたプロジェクト)。 「[/O オプション (コードの最適化)](https://msdn.microsoft.com/library/77997af9-5555-4b3d-aa57-6615b27d4d5d)」を参照してください)。 これにはローカル変数とインライン関数のデバッグのサポートの強化が含まれます。  
>   
> [エディット コンティニュ](../debugger/edit-and-continue-visual-csharp.md)は、 **/Zo** コンパイラ オプションを使用している場合は無効です。  
  
 コンパイラは、ソース コードを最適化するときに命令を再配置したり再構成したりします。 これにより、コンパイル後のコードの実行効率が向上します。 しかし、この命令の整理が原因となり、一連の命令に対応するソース コードをデバッガーが識別できなくなる場合があります。  
  
 最適化によって次のような影響が生じる場合があります。  
  
- ローカル変数がオプティマイザーによって削除されたり、デバッガーの追跡できない場所に移動されたりする可能性があります。  
  
- オプティマイザーによってコード ブロックがマージされた場合、関数内の位置が変更されます。  
  
- オプティマイザーによって 2 つの関数がマージされた場合、呼び出し履歴上のフレームに対し、間違った関数名が表示される場合があります。  
  
  ほとんどの場合、呼び出し履歴上のフレームには、正しい情報が表示されます。ただし、これはすべてのフレームにシンボルが割り当てられていることが前提です。 スタックの破損が生じた場合、アセンブリ言語で記述された関数が存在する場合、呼び出し履歴上のシンボルに一致しないオペレーティング システムのフレームが存在する場合など、呼び出し履歴上のフレームに誤った情報が表示されることがあります。  
  
  グローバル変数および静的変数は常に正しく表示されます。 構造体レイアウトについても同様です。 構造体へのポインターが存在し、そのポインターの値が正しければ、構造体のすべてのメンバー変数は、正しい値で表示されます。  
  
  これらの制限事項のため、できるだけ最適化する前のプログラムをデバッグするようにしてください。 既定では、最適化に対する設定は、Visual C++ プログラムのデバッグ構成ではオフ、リリース構成ではオンになっています。  
  
  ただし、最適化後のプログラムでしかバグが発生しない場合もあります。 このような場合は、最適化されたコードをデバッグする必要があります。  
  
### <a name="to-turn-on-optimization-in-a-debug-build-configuration"></a>デバッグ ビルド構成で最適化をオンにするには  
  
1. 新しいプロジェクトの作成時に、`Win32 Debug` ターゲットを選択します。 プログラムが完全にデバッグされ、`Win32 Release` ターゲットをビルドできるようになるまでは、`Win32``Debug` ターゲットを使用します。 コンパイラは、`Win32 Debug` ターゲットの最適化は行いません。  
  
2. ソリューション エクスプローラーでプロジェクトを選択します。  
  
3. **[表示]** メニューの **[プロパティ ページ]** をクリックします。  
  
4. **[プロパティ ページ]** ダイアログ ボックスで、 **[構成]** ボックスの [`Debug`] が選択されていることを確認します。  
  
5. 左側のフォルダー ビューで、 **[C/C++]** フォルダーを選択します。  
  
6. **[C/C++]** フォルダーの下の [`Optimization`] を選択します。  
  
7. 右側のプロパティ リストで、[`Optimization`] を探します。 その横の設定値は、`Disabled (`[/Od](https://msdn.microsoft.com/library/b1ac31b7-e086-4eeb-be5e-488f7513f5f5)`)` になっているはずです。 その他のオプション (`Minimum Size``(`[/O1](https://msdn.microsoft.com/library/2d1423f5-53d9-44da-8908-b33a351656c2)`)`、`Maximum Speed``(`[/O2](https://msdn.microsoft.com/library/2d1423f5-53d9-44da-8908-b33a351656c2)`)`、`Full Optimization``(`[/Ox](https://msdn.microsoft.com/library/3ad7c30b-c615-428c-b1d0-2e024f81c760)`)`、`Custom`) から 1 つを選択します。  
  
8. [`Custom`] に対して [`Optimization`] オプションを選択すると、プロパティ リストに表示されているその他のプロパティについてオプションを設定できるようになります。  
  
9. プロジェクトのプロパティ ページの [構成プロパティ]、[C/C++]、[コマンド ライン] ノードを選択し、`(`[/Zo](https://msdn.microsoft.com/library/eea8d89a-7fe0-4fe1-86b2-7689bbebbd7f)`)` を **[その他のオプション]** テキスト ボックスに追加します。  
  
    > [!WARNING]
    > `/Zo` には、Visual Studio 2013 更新プログラム 3 以降のバージョンが必要です。  
    >   
    >  `/Zo` を追加すると、[エディット コンティニュ](../debugger/edit-and-continue-visual-csharp.md)が無効になります。  
  
   最適化されたコードをデバッグするときは、 **[逆アセンブリ]** ウィンドウを使用して実際にどのような命令が作成および実行されているのかを確認してください。 ブレークポイントを設定する場合は、ブレークポイントが命令と共に移動する可能性があるため注意が必要です。 次に例を示します。  
  
```  
for (x=0; x<10; x++)  
```  
  
 この行にブレークポイントを設定したとします。 ブレークポイントは 10 回ヒットするように思われますが、このコードを最適化した場合、ブレークポイントは 1 回しかヒットしません。 これは、最初の命令によって `x` の値が 0 に設定されるためです。 コンパイラは、その最初の命令を 1 回だけ実行すると見なしてループの外に移動します。 このとき、ブレークポイントもこの命令と共に移動します。 `x` を比較してインクリメントする命令はループ内に残ったままになります。 **[逆アセンブリ]** ウィンドウを参照すると、コードの実行をより細かく制御できるように、[ステップ実行の単位](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9)が自動的に命令に設定されています。この設定は、最適化されたコードをステップ実行するときに役立ちます。  
  
## <a name="see-also"></a>参照  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
