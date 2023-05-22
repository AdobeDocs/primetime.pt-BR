---
title: Visão geral do servidor de licenças e do empacotador de pastas monitoradas
description: Visão geral do servidor de licenças e do empacotador de pastas monitoradas
copied-description: true
exl-id: 1a355068-7ad6-4cc2-8447-49251dae3ff8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Visão geral do servidor de licenças e do empacotador de pastas monitoradas {#license-server-and-watched-folder-packager-overview}

O servidor de implementação de referência pode ajudar você a criar um servidor de licença usando o SDK de acesso ao Adobe. Nesta implementação, os usuários são autenticados com base nas entradas do usuário em um banco de dados. O servidor inclui lógica de negócios de demonstração para emitir licenças. Ele também implementa o suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

O servidor de implementação de referência também inclui uma implementação de pasta monitorada do empacotador. Esse componente pode ser implantado junto com o servidor de licenças ou em um computador separado. Com essa implementação do empacotador, várias pastas monitoradas podem ser criadas. Quando o conteúdo é colocado na pasta monitorada, o empacotador automaticamente compacta o conteúdo.

O servidor de licenças e o empacotador são implantados como arquivos WAR separados, para que você possa escolher se deseja executá-los em servidores separados ou em uma única instância Apache Tomcat®. O servidor de licença está no estado [!DNL flashaccess.war] e o empacotador estiver em [!DNL flashaccess-packager.war]. O modelo opcional [!DNL edcws.war] contém suporte para solicitações de licença de clientes FMRMS 1.x.

O código de amostra da Implementação de referência demonstra os seguintes recursos:

* Servidor de licenças:

   * Lidar com solicitações de autenticação, usando um banco de dados para validar o nome de usuário/senha
   * Lidar com solicitações de licença e determinar que tipo de licença emitir quando o encadeamento de licenças for usado.
   * Emissão de licenças para conteúdo que contém várias políticas
   * Emitir licenças que oferecem suporte à entrega de Chave remota para clientes do iOS (exige o Adobe Primetime)
   * Emissão de licenças que exigem uma pesquisa/recuperação externa da Chave de criptografia de conteúdo (CEK)
   * Utilização do banco de dados para determinar se o usuário está autorizado a visualizar conteúdo
   * Uso de listas de atualização de política
   * Usando listas de revogação de computador
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografando senhas especificadas no arquivo de propriedades
   * Especificação de várias credenciais de servidor de licença ou de transporte (após a renovação das credenciais, as credenciais antigas são mantidas no servidor para que o conteúdo existente possa ser consumido sem a necessidade de reempacotar)
   * Restrição de versões de DRM/Runtime permitidas para fazer solicitações ao servidor de licença
   * Definição das preferências de windback do relógio do cliente
   * Restrição da diferença de tempo permitida entre o tempo de solicitação e o tempo do servidor (para impedir ataques de repetição)
   * Lidar com solicitações de clientes FMRMS 1.x (aciona o cliente FMRMS 1.x para atualizar para o Adobe Access 2.0 ou posterior)
   * Conversão de metadados do FMRMS 1.x para metadados de Acesso Adobe em tempo real, usando informações de licença do FMRMS 1.x armazenadas em um banco de dados
   * Exemplo de código para converter políticas do FMRMS 1.x em políticas de acesso de Adobe
   * Exemplos de scripts para importação de informações de licença do FMRMS 1.x de um banco de dados existente
   * Obter Versão do Servidor
   * Registro de domínio
   * Cancelamento de registro de domínio
   * Solicitações de sincronização
   * Devolução de licença

* Servidor do empacotador:

   * Implementação de uma implementação do empacotador que empacota automaticamente o conteúdo adicionado a uma pasta monitorada
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografando senhas especificadas no arquivo de propriedades
   * Configurar o empacotador, criar políticas e criar listas de atualização de políticas usando um aplicativo do AIR
