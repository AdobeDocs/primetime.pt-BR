---
title: SSO no iOS ao usar o Criador de acesso de autenticação do Primetime
description: SSO no iOS ao usar o Criador de acesso de autenticação do Primetime
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# SSO no iOS ao usar o Criador de acesso de autenticação do Primetime {#sso-on-ios-when-using-the-primetime-authentication-access-enabler}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Visão geral

O Logon único (SSO) entre aplicativos com autenticação do Primetime funciona de maneiras diferentes, dependendo do sistema operacional subjacente.

Endereços deste documento **SSO no iOS**, ao usar a autenticação do Adobe Primetime **Ativador de acesso**.

**Ativador de acesso** **1,10** é a versão mais recente do SDK nativo da iOS de autenticação da Adobe Primetime. O Adobe recomenda que você migre para essa versão em vez de ficar com uma versão mais antiga. Se estiver usando uma versão mais antiga do Ativador de acesso, você pode baixar a versão mais recente [here](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library).

O SSO no iOS é ditado pelas seguintes condições:

- Os aplicativos devem usar o mesmo **armazenamento de token** (na forma de uma área de transferência personalizada criada pelo Ativador de acesso).
- Os aplicativos devem gerar o mesmo **ID do dispositivo** (O Access Enabler calcula a ID do dispositivo com base no endereço MAC ou no IDFV, dependendo da versão do SO).

## Comportamento

O comportamento do SSO é o seguinte:

- **iOS 6 e inferior**: O SSO funciona automaticamente entre aplicativos desenvolvidos pela mesma equipe ou por equipes diferentes. A ID do dispositivo é calculada com base no endereço do MAC (o mesmo valor é produzido em todos os aplicativos) e a área de armazenamento é comum a todos os aplicativos (a área de transferência personalizada pode ser compartilhada entre aplicativos no iOS 6 e inferior).
   - **Importante:** Observe que a versão 1.9.4 do SDK do iOS tem [o direcionamento mínimo de implantação do iOS foi aumentado para o iOS 7.](https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library) 
- **iOS 7 e superior**: O SSO funcionará nas seguintes condições:

1. Os aplicativos são publicados usando o mesmo perfil de distribuição do Apple ou perfis que pertencem à mesma equipe. Essa é a única maneira de os aplicativos compartilharem pasteboards personalizadas no iOS 7 e superior. Em todos os outros cenários, a área de transferência é restrita por aplicativo. De [*https://developer.apple.com/library/IOs/releasenotes/General/RN-iOSSDK-7.0/index.html*](https://developer.apple.com/library/ios/releasenotes/General/RN-iOSSDK-7.0/index.html): \+\[ÁreaÁreaInicialUIPasteboardWithName:create:\] e +\[UIPasteboardWithUniqueName\] agora excluem o nome fornecido para permitir que apenas os aplicativos no mesmo grupo de aplicativos acessem a área de transferência. Se o desenvolvedor tentar criar uma área de transferência com um nome que já existe e que não faz parte do mesmo conjunto de aplicativos, ela receberá sua própria área de trabalho exclusiva e privada. Observe que isso não afeta as áreas de trabalho fornecidas pelo sistema, geral e localizar.

1. Os aplicativos têm o mesmo prefixo de ID de pacote (todos os componentes, exceto o último). Somente os aplicativos que compartilham o mesmo prefixo de ID de pacote calcularão o mesmo IDFV. De [*https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice\_Class/index.html\#//apple\_ref/occ/instp/UIDevice/identifierForVendor*](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIDevice_Class/index.html#//apple_ref/occ/instp/UIDevice/identifierForVendor): No IOS 7, todos os componentes do pacote, exceto o último componente, são usados para gerar a ID do fornecedor. Se a ID do pacote tiver apenas um componente, toda a ID do pacote será usada.

Vamos agora focar no **&quot;iOS 7 e superior&quot;** já que é a mais frequente para usuários reais:

Ambas as condições (compartilhar um perfil da mesma equipe de desenvolvimento e ter um prefixo comum de identificador de pacote) são condições obrigatórias para o SSO.

Estas são as combinações possíveis e seus resultados gerados:

- **Perfis da mesma equipe e o mesmo prefixo da ID do pacote**: os aplicativos compartilharão o mesmo armazenamento na área de transferência e terão a mesma ID do dispositivo (IDFV). Um usuário precisará se autenticar apenas uma vez (no primeiro aplicativo usado) e o estado de autenticação será compartilhado em todos os outros aplicativos. Exemplo de fluxo:

1. O usuário abre o aplicativo A (com ID do pacote) *com.x.y.AppA*) e não está autenticado
1. O usuário realiza autenticação no aplicativo A
1. O usuário abre o aplicativo B (com ID do pacote) *com.x.y.AppB*) e é automaticamente autenticado ao compartilhar os dados de direito do aplicativo A (da etapa 2)
1. O usuário abre o aplicativo A e ainda é autenticado (da etapa 2)

 

- **Perfis da mesma equipe, mas prefixos de ID do pacote diferentes**: os aplicativos compartilharão o mesmo armazenamento na área de transferência, mas terão IDs de dispositivo diferentes (IDFVs). Um usuário precisará se autenticar uma vez para cada aplicativo. Exemplo de fluxo:

1. O usuário abre o aplicativo A (com ID do pacote) *com.x.y.AppA*) e não está autenticado
1. O usuário realiza autenticação no aplicativo A
1. O usuário abre o aplicativo B (com ID do pacote) *com.z.AppB*) e o Access Enabler detecta o token obtido pelo primeiro aplicativo (porque o armazenamento é compartilhado), mas não tentará usá-lo via SSO devido às diferentes IDs do dispositivo
1. O usuário realiza autenticação no aplicativo B
1. O usuário abre o aplicativo A e ainda é autenticado (da etapa 2)

 

- **Perfis de equipes diferentes (a ID do pacote é irrelevante neste cenário)**: os aplicativos terão diferentes armazenamentos de área de transferência e o SSO será desativado entre eles. Um usuário precisará se autenticar uma vez para cada aplicativo e as sessões de autenticação permanecerão persistentes ao alternar entre aplicativos. Exemplo de fluxo:


1. O usuário abre o aplicativo A e não é autenticado
1. O usuário realiza autenticação no aplicativo A
1. O usuário abre o aplicativo B e não é autenticado
1. O usuário realiza autenticação no aplicativo B
1. O usuário abre o aplicativo A e é autenticado (da etapa 2)
1. O usuário abre o aplicativo B e é autenticado (da etapa 4)

**Observação:** Observe que as condições acima para SSO são aplicáveis ao instalar aplicativos por meio do **Apple App Store**. Se os aplicativos forem implantados em um simulador (onde a assinatura do aplicativo não se aplica), instalado com o Xcode ou distribuído por um perfil Ad Hoc, você poderá obter resultados diferentes.

**Importante:** Observação (**sobre o AccessEnabler v1.8**): O segundo cenário descrito acima (perfis da mesma equipe, mas prefixos de ID de pacote diferentes) criará uma experiência de usuário muito desagradável para os usuários do **AccessEnabler v1.8** em aplicativos desenvolvidos pela mesma equipe (empresa de mídia). O usuário será desconectado automaticamente durante a transição entre aplicativos da mesma empresa de mídia, portanto, os desenvolvedores de aplicativos devem tomar cuidado ao decidir a ID do pacote e o perfil de distribuição. O cenário exato nesse caso é apresentado abaixo:

Os aplicativos compartilharão o mesmo armazenamento na área de transferência, mas terão IDs de dispositivo diferentes (IDFVs). Um usuário precisará se autenticar uma vez para cada aplicativo, **mas as sessões de autenticação serão apagadas ao alternar entre aplicativos**. Exemplo de fluxo:

1. O usuário abre o aplicativo A (com ID do pacote) *com.x.y.AppA*) e não está autenticado
1. O usuário realiza autenticação no aplicativo A
1. O usuário abre o aplicativo B (com ID do pacote) *com.z.AppB*) e os dados de direito criados pelo aplicativo A são automaticamente apagados pelo Ativador de acesso (mecanismo de segurança que detecta um conflito entre a ID de dispositivo atualmente computada no aplicativo B e a que está armazenada nos tokens de direito - criado pelo aplicativo A)
1. O usuário realiza autenticação no aplicativo B
1. O usuário abre o aplicativo A e os dados de direito criados pelo aplicativo B são automaticamente apagados pelo Ativador de acesso (mecanismo de segurança que detecta um conflito entre a ID de dispositivo atualmente computada no aplicativo A e a que está armazenada nos tokens de direito - criado pelo aplicativo B)

