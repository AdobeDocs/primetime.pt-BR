---
title: Terminologia e conceitos principais
description: Terminologia e conceitos principais
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Terminologia e conceitos principais {#terminology-and-core-concepts}

Os termos e conceitos a seguir são usados neste documento:

**Consumidor**

A variável *consumidor* é o usuário final que baixa ou transmite conteúdo.

**Conteúdo**

*Conteúdo* consiste em arquivos de áudio ou vídeo digital.

**Chave de criptografia do conteúdo**

A variável *Chave de criptografia do conteúdo* (CEK) é uma chave criptográfica usada para criptografar o conteúdo.

**Proprietários do conteúdo**

*Proprietários do conteúdo* são as entidades comerciais que detêm os direitos autorais do conteúdo. Podem ser grandes estúdios de cinema, ou pequenos produtores independentes de filmes ou outros conteúdos audiovisuais.

**Empacotadores de conteúdo**

*Empacotadores de conteúdo* são organizações que empacotam conteúdo para uso com o Adobe Access. Os proprietários ou distribuidores de conteúdo podem optar por empacotar seu próprio conteúdo ou podem solicitar os serviços de terceiros para empacotar seu conteúdo e distribuí-lo eletronicamente pela Internet.

**Certificado digital**

*Certificados digitais* (também referido como *certificados*) vincular uma entidade, como um indivíduo, organização ou sistema, a um par de chaves público e privado específico. Certificados digitais podem ser considerados credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

**Assinatura digital**

A *assinatura digital* vincula a identidade do publicador ao conteúdo publicado e fornece um mecanismo para detectar adulterações. Os algoritmos de assinatura digital usam funções de hash criptográfico e algoritmos de criptografia assimétricos ou de par de chaves públicas/privadas. Algumas assinaturas digitais também aproveitam os certificados digitais e a infraestrutura de chave pública (PKI) para vincular chaves públicas às identidades de proprietários ou distribuidores de conteúdo.

**Distribuidor**

*Distribuidores* (também referido como *distribuidores de conteúdo* ou* varejistas*) são entidades comerciais que protegem os direitos de distribuição dos proprietários do conteúdo para publicar e distribuir conteúdo aos consumidores. Em alguns casos, a mesma entidade é o proprietário do conteúdo e o distribuidor de conteúdo.

**Metadados de DRM**

Informações que o cliente (ou seja, o Adobe® Flash® Player, o tempo de execução do Adobe® AIR® e o cliente Primetime) envia para identificar o conteúdo solicitado.

**Licença**

Uma *licença *é uma estrutura de dados que contém uma chave criptografada usada para descriptografar o conteúdo associado a uma política. A licença é gerada pelo Adobe Access quando o consumidor solicita conteúdo e está vinculada ao computador do consumidor. Usando uma política como referência, a licença define os direitos disponíveis para o consumidor que baixa o conteúdo. Para visualizar o conteúdo, o consumidor deve obter uma licença.

**Aquisição de licença**

*Aquisição de licença* é o processo de aquisição de uma licença que permite ao consumidor descriptografar e visualizar o conteúdo protegido de acordo com um conjunto de regras de uso. A aquisição de licença ocorre quando um cliente envia informações que identificam o conteúdo solicitado (o *Metadados de DRM*) e o certificado da máquina (identificando o computador do consumidor) para o License Server (veja abaixo).

**Servidor de licenças**

O * License Server * pode ser integrado aos sistemas de faturamento e autenticação do distribuidor ou provedor de serviços e pode conter lógica de negócios para verificar se o consumidor que solicita o conteúdo protegido está autorizado a visualizá-lo. Se o usuário estiver autorizado a acessar o conteúdo, o License Server emitirá uma licença permitindo que o cliente de tempo de execução descriptografe e reproduza o conteúdo com base na política e nos direitos associados à conta do consumidor.

Você deve criar e implantar um License Server usando o SDK de acesso ao Adobe.

**Política**

A *política* é um container para as regras de uso que determinam como os consumidores podem usar o conteúdo protegido. As políticas são definidas independentemente do conteúdo que está sendo protegido. Uma política não impõe direitos até que seja vinculada ao conteúdo por meio da licença. Uma política lista o conjunto de regras de uso, o que significa as permissões ou os &quot;direitos&quot; que os consumidores têm sobre o conteúdo que adquirem. Por exemplo, os proprietários de conteúdo podem criar uma política que garanta que o conteúdo protegido só seja acessível aos consumidores por um período específico. Essa política é então aplicada a todo o conteúdo para o qual o proprietário do conteúdo deseja aplicar essa restrição.

As políticas são criadas usando o SDK de acesso do Adobe.

**Conteúdo protegido**

*Conteúdo protegido* (também referido como *conteúdo empacotado*) refere-se ao conteúdo de vídeo FLV e F4V que foi criptografado usando o SDK do Adobe Access ou outras ferramentas compatíveis.

**Varejistas**

Consulte a entrada para *distribuidores* anteriormente nesta seção.
