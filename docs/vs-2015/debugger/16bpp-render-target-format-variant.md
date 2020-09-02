---
title: 16 bpp レンダリング ターゲット フォーマット バリアント | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7b315c7ab9bb10d039e81ba26b1beb9c4447a205
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157571"
---
# <a name="16bpp-render-target-format-variant"></a>16bpp レンダリング ターゲット フォーマット バリアント
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

すべてのレンダー ターゲットおよびバック バッファーに対して、ピクセル形式を DXGI_FORMAT_B5G6R5_UNORM に設定します。  
  
## <a name="interpretation"></a>解釈  
 レンダー ターゲットまたはバック バッファーは通常、B8G8R8A8_UNORM などの 32bpp (32 ビット (ピクセルあたり)) 形式を使用します。 32bpp 形式は、大量のメモリ帯域幅を消費します。 B5G6R5_UNORM 形式は 32bpp 形式の半分の 16bpp 形式であるため、これを使用してメモリ帯域幅における消費を緩和することができますが、色の忠実性は低下します。  
  
 このバリアントによりパフォーマンスが大幅に向上する場合は、おそらくアプリケーションで使用しているメモリ帯域幅が多すぎることを示しています。 プロファイルされたフレームで描画の大きさが問題になる場合、または多数のアルファブレンディングが含まれている場合は、著しくパフォーマンスが向上することがあります。  
  
 アプリケーションでレンダリングされるシーンで色を忠実に再現する必要がない場合、レンダー ターゲットでアルファ チャネルを持つ必要がない場合、および滑らかなグラデーションがそれほど必要ない場合 (これらのケースは色の忠実性が低い場合には、連結している成果物の影響を受けやすい) は、16bpp レンダー ターゲット形式を使用してメモリ帯域幅の使用を減らすことを検討します。  
  
 アプリケーションでレンダリングされるシーンで色を忠実に再現する必要がある場合、アルファ チャネルが必要な場合、または滑らかなグラデーションを多用している場合は、メモリ帯域幅の使用を減らすために他の方法を検討します (たとえば描画の大きさを小さくする、アルファブレンディングを減らす、フレームバッファーのディメンションを少なくする、テクスチャ リソースを修正し、圧縮または次元を減らすことによってメモリ帯域幅の使用を減らす、などの方法があります)。 これらの方法のいずれかを最適化することとイメージの品質を保持することは背反するため、通常と同じように両者のバランスを考慮する必要があります。  
  
 16bpp のバック バッファーへ切り替えることによりアプリケーションでメリットが生じるけれども、スワップ チェーンの一部となる場合は、追加の手順が必要になります。`D3D11CreateDeviceAndSwapChain` または `IDXGIFactory::CreateSwapChain` を使用して作成されたスワップ チェーンについては、DXGI_FORMAT_B5G6R5_UNORM はサポートされているバック バッファー形式ではないためです。 代わりに、`CreateTexture2D` を使用して B5G6R5_UNORM 形式のレンダー ターゲットを作成し、レンダリングします。 ここでスワップ チェーンで Present を呼び出す前に、レンダー ターゲットをソース テクスチャとしてフルスクリーン クアッドを描画して、スワップ チェーンのバック バッファー上にレンダー ターゲットをコピーします。 これは特別な手順で多少のメモリ帯域幅を消費しますが、大半のレンダリング処理では 16bpp のレンダー ターゲットに影響を与えるため、消費する帯域幅はもっと少なくなります。これにより、レンダー ターゲットをスワップ チェーンのバック バッファーにコピーするときに消費される帯域幅よりも多くの帯域幅が節約されると、レンダリングのパフォーマンスは改善されます。  
  
 タイル型のレンダリング テクニックを使用する GPU アーキテクチャでは、16bpp フレームバッファー形式の使用によりパフォーマンスが著しく改善されます。これは、フレームバッファーのより大きい領域が、タイル型の各ローカル フレームバッファー キャッシュに適合するためです。 タイル型のレンダリング アーキテクチャは、携帯電話機やタブレット コンピューターの GPU で使用されています。これらの市場以外で使用されることはほとんどありません。  
  
## <a name="remarks"></a>Remarks  
 レンダー ターゲット形式は、レンダー ターゲットを作成する `ID3D11Device::CreateTexture2D` への呼び出しのたびに、DXGI_FORMAT_B5G6R5_UNORM にリセットされます。 具体的には、pDesc で渡される D3D11_TEXTURE2D_DESC オブジェクトがレンダー ターゲットを記述するときに、この形式はオーバーライドされます。つまり、  
  
- BindFlags メンバーは、D3D11_BIND_REDNER_TARGET フラグを設定します。  
  
- BindFlags メンバーは D3D11_BIND_DEPTH_STENCIL フラグを解除します。  
  
- Usage メンバーは D3D11_USAGE_DEFAULT に設定されます。  
  
## <a name="restrictions-and-limitations"></a>制約と制限  
 B5G6R5 形式ではアルファ チャネルを持たないため、アルファ コンテンツはこのバリアントでは保存されません。 アプリケーションのレンダリングで、レンダー ターゲットのアルファ チャネルが必要な場合、B5G6R5 形式に切り替えることはできません。  
  
## <a name="example"></a>例  
 次のようなコードを使用して、を使用して作成されたレンダーターゲットに対して、 **16bpp レンダーターゲット形式** バリアントを再現でき `CreateTexture2D` ます。  
  
```  
D3D11_TEXTURE2D_DESC target_description;  
  
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;  
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;  
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);  
```
