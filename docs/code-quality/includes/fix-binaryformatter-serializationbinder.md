---
ms.openlocfilehash: 557d811e2eeaf926cb958471d214fc23c50a25f2
ms.sourcegitcommit: 43df639b2cd99200f725a8ebb941477481a6f0ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87471579"
---
- 代わりに、セキュリティで保護されたシリアライザーを使用して、**攻撃者が任意の型を逆シリアル化することを許可しないよう**にします。 詳細については、推奨される[代替手段](/dotnet/standard/serialization/binaryformatter-security-guide#preferred-alternatives)を参照してください。
- シリアル化されたデータの改ざん防止を行います。 シリアル化後に、シリアル化されたデータに暗号署名します。 逆シリアル化する前に、暗号化署名を検証します。 暗号化キーが公開され、キーのローテーションのための設計になっていないことを防止します。
- このオプションを使用すると、サービス拒否攻撃やリモートのコード実行攻撃に対してコードが脆弱になります。 詳細については、「 [Binaryformatter セキュリティガイド](/dotnet/standard/serialization/binaryformatter-security-guide)」を参照してください。 逆シリアル化された型を制限します。 カスタムを実装 <xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType> します。 逆シリアル化する前に、 `Binder` すべてのコードパスで、プロパティをカスタムのインスタンスに設定し <xref:System.Runtime.Serialization.SerializationBinder> ます。 オーバーライドされたメソッドで、型が予期しない場合は例外をスローして、 <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> 逆シリアル化を停止します。
