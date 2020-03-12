---
seo-title: Visão geral do servidor de licenças e do empacotador de pastas observado
title: Visão geral do servidor de licenças e do empacotador de pastas observado
uuid: 3dd6f699-a5c0-44c4-897a-34e06abe3d71
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visão geral do servidor de licenças e do empacotador de pastas observado {#license-server-and-watched-folder-packager-overview}

O servidor de implementação de referência pode ajudá-lo a criar um servidor de licenças usando o SDK do Adobe Access. Nesta implementação, os usuários são autenticados com base em entradas de usuários em um banco de dados. O servidor inclui lógica comercial de demonstração para a emissão de licenças. Ele também implementa o suporte de compatibilidade para o Flash Media Rights Management Server 1.0 e 1.5.

O servidor de implementação de referência também inclui uma implementação de pasta assistida do empacotador. Esse componente pode ser implantado junto com o servidor de licenças ou em uma máquina separada. Com essa implementação do Packager, várias pastas monitoradas podem ser criadas. Quando o conteúdo é descartado na pasta assistida, o empacotador automaticamente agrupa o conteúdo.

O servidor de licenças e o empacotador são implantados como arquivos WAR separados, de modo que você pode optar por executá-los em servidores separados ou em uma única instância do Apache Tomcat®. O servidor de licenças está no e o empacotador [!DNL flashaccess.war] está no [!DNL flashaccess-packager.war]. O opcional [!DNL edcws.war] contém suporte para solicitações de licença de clientes FMRMS 1.x.

O código de exemplo de Implementação de referência demonstra os seguintes recursos:

* Servidor de licença:

   * Tratamento de solicitações de autenticação, uso de um banco de dados para validar nome de usuário/senha
   * Tratamento de solicitações de licença e determinação do tipo de licença a ser emitido quando o encadeamento de licença for usado.
   * Emissão de licenças para conteúdo que contém várias políticas
   * Emita licenças que oferecem suporte à entrega da chave remota para clientes iOS (requer o Adobe Primetime)
   * Emissão de licenças que exigem pesquisa/recuperação externa da Chave de criptografia de conteúdo (CEK)
   * Usar o banco de dados para determinar se o usuário está autorizado a exibir o conteúdo
   * Uso de listas de atualização de política
   * Usando listas de revogação de máquina
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografar senhas especificadas no arquivo de propriedades
   * Especificação de várias credenciais de servidor de licenças ou de transporte (depois que as credenciais são renovadas, as credenciais antigas são mantidas no servidor para que o conteúdo existente possa ser consumido sem a necessidade de reempacotar)
   * A restrição de versões DRM/Runtime permite fazer solicitações ao servidor de licenças
   * Configuração das preferências de retorno de tempo do relógio do cliente
   * Restrição da diferença de tempo permitida entre o tempo da solicitação e o tempo do servidor (para evitar ataques de repetição)
   * Tratamento de solicitações de clientes FMRMS 1.x (aciona o cliente FMRMS 1.x para atualizar para o Adobe Access 2.0 ou posterior)
   * Convertendo metadados FMRMS 1.x em metadados do Adobe Access dinamicamente, usando informações de licença FMRMS 1.x armazenadas em um banco de dados
   * Exemplo de código para converter políticas FMRMS 1.x em políticas do Adobe Access
   * Scripts de amostra para importar informações de licença do FMRMS 1.x de um banco de dados existente
   * Obter versão do servidor
   * Registro de domínio
   * Cancelamento de registro no domínio
   * Solicitações de sincronização
   * Devolução de licença

* Servidor Packager:

   * Implementação de uma implementação do Packager que automaticamente agrupa o conteúdo adicionado a uma pasta assistida
   * Uso de um arquivo HSM ou PKCS12 para armazenar credenciais
   * Criptografar senhas especificadas no arquivo de propriedades
   * Configurar o empacotador, criar políticas e criar listas de atualização de política usando um aplicativo AIR

