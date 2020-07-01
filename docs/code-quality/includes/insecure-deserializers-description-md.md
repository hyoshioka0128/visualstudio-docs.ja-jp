---
author: dotpaul
ms.author: paulming
ms.date: 04/05/2019
ms.topic: include
ms.openlocfilehash: 054198eff46c0983a5610b29dee5e29e5ac67a70
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68147094"
---
安全でないデシリアライザーは、信頼できないデータを逆シリアル化するときに脆弱です。 攻撃者は、悪意のある副作用を持つオブジェクトを挿入するために、シリアル化されたデータを変更し、予期しない型を含めることができます。 セキュリティで保護されていないデシリアライザーに対する攻撃は、たとえば、基になるオペレーティングシステムでコマンドを実行したり、ネットワークを介して通信したり、ファイルを削除したりすることができます。