---
title: Visão geral do servidor de licenças e do pacote de pastas monitoradas
description: Visão geral do servidor de licenças e do pacote de pastas monitoradas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Visão geral do servidor de licenças e do pacote de pastas monitoradas {#license-server-and-watched-folder-packager-overview}

O servidor de implementação de referência pode ajudá-lo a criar um servidor de licenças usando o SDK de Acesso ao Adobe. Nesta implementação, os usuários são autenticados com base nas entradas do usuário em um banco de dados. O servidor inclui lógica comercial de demonstração para a emissão de licenças. Ele também implementa o suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

O servidor de implementação de referência também inclui uma implementação de pasta monitorada do empacotador. Esse componente pode ser implantado junto com o servidor de licenças ou em uma máquina separada. Com essa implementação do empacotador, várias pastas monitoradas podem ser criadas. Quando o conteúdo é descartado na pasta assistida, o empacotador compacta automaticamente o conteúdo.

O servidor de licenças e o empacotador são implantados como arquivos WAR separados, de modo que você pode optar por executá-los em servidores separados ou em uma única instância do Apache Tomcat®. O servidor de licenças está no [!DNL flashaccess.war] e o empacotador está em [!DNL flashaccess-packager.war]. O [!DNL edcws.war] opcional contém suporte para solicitações de licença de clientes FMRMS 1.x.

O código de exemplo de Implementação de referência demonstra os seguintes recursos:

* Servidor de licenças:

   * Tratamento de solicitações de autenticação, uso de um banco de dados para validar nome de usuário/senha
   * Tratamento de pedidos de licenças e determinação do tipo de licença a emitir quando é utilizado o encadeamento de licenças.
   * Emitir licenças para conteúdo contendo várias políticas
   * Emita licenças que oferecem suporte para o delivery de chave remota para clientes iOS (requer Adobe Primetime)
   * Emitir licenças que exigem pesquisa/recuperação externa da Chave de criptografia de conteúdo (CEK)
   * Uso do banco de dados para determinar se o usuário está autorizado a exibir conteúdo
   * Uso de listas de atualização de política
   * Usando listas de revogação de máquina
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografar senhas especificadas no arquivo de propriedades
   * Especificar vários servidores de licenças ou credenciais de transporte (após a renovação das credenciais, as credenciais antigas serão mantidas no servidor para que o conteúdo existente possa ser consumido sem a necessidade de reempacotar)
   * Restrição de versões DRM/Runtime permitidas para fazer solicitações ao servidor de licenças
   * Definindo as preferências de retorno do relógio do cliente
   * Restrição da diferença de tempo permitida entre o tempo da solicitação e o tempo do servidor (para evitar ataques de repetição)
   * Lidar com solicitações de clientes FMRMS 1.x (aciona o cliente FMRMS 1.x para atualizar para o Adobe Access 2.0 ou posterior)
   * Convertendo metadados FMRMS 1.x em metadados de Adobe Access instantaneamente, usando informações de licença FMRMS 1.x armazenadas em um banco de dados
   * Exemplo de código para converter políticas FMRMS 1.x em políticas de acesso ao Adobe
   * Exemplos de scripts para importar informações de licença do FMRMS 1.x de um banco de dados existente
   * Obter Versão do Servidor
   * Registro de domínio
   * Cancelamento do registro de domínio
   * Solicitações de sincronização
   * Devolução de licença

* Servidor do Empacotador:

   * Implementação de um empacotador que compacta automaticamente o conteúdo adicionado a uma pasta assistida
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografar senhas especificadas no arquivo de propriedades
   * Configuração do empacotador, criação de políticas e criação de listas de atualização de política usando um aplicativo AIR

