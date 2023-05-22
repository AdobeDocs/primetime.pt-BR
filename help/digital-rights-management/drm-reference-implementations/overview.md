---
title: Sobre as implementações de referência
description: Sobre as implementações de referência
copied-description: true
exl-id: fe387330-9449-4977-be15-069c814354bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# Sobre as implementações de referência{#about-the-reference-implementations}

Este guia descreve a instalação, a configuração e a operação das implementações de referência do DRM da Adobe Primetime.

>[!NOTE]
>
>O DRM do Primetime era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

As implementações de referência de DRM do Primetime incluem estes componentes:

* **Ferramentas de linha de comando** - Essas ferramentas se baseiam no mesmo código de SDK DRM do Primetime usado no servidor de licença DRM do Primetime. Você pode executar empacotamento, licenciamento e outras tarefas de DRM a partir da linha de comando e alternar facilmente entre o uso das ferramentas de linha de comando e o servidor de licenças.
* **Servidor de licenças** - Um servidor de licenças totalmente funcional e personalizável (descrito abaixo como uma das opções do seu servidor de licenças).

**Opções do Servidor de Licença:**

* **As implementações de referência do DRM do Primetime** - O assunto deste guia, essa implementação de referência apresenta um servidor de licença DRM robusto que mostra todos os recursos fornecidos pelo SDK DRM do Primetime. Essa implementação é fornecida com o código-fonte e instruções para a criação do código. Esta implementação não se destina a ser usada como está (embora uma [!DNL .war] arquivo que você pode implantar rapidamente). Ela serve principalmente como uma referência que você pode usar para criar seu próprio servidor de licença personalizado.

   Recursos do Servidor de Licença:

   * Gerencia solicitações de autenticação usando um banco de dados para validar o nome de usuário/senha.
   * Gerencia solicitações de licença e determina o tipo de licença que está sendo emitida quando o encadeamento de licenças é aplicado.
   * Emite licenças para conteúdo que inclui várias políticas de DRM do Primetime.
   * Emite licenças que oferecem suporte à entrega de Chave remota para clientes iOS, o que requer o DRM do Primetime.
   * Emite licenças que exigem uma pesquisa e recuperação externas da Chave de Criptografia de Conteúdo (CEK).
   * Pesquisa um banco de dados para determinar se um usuário está autorizado a visualizar conteúdo.
   * Pesquisa listas de atualização de política DRM do Primetime.
   * Pesquisa listas de revogação de computador.
   * Usa um arquivo HSM ou PKCS12 para armazenar credenciais.
   * Criptografa senhas especificadas em um arquivo de propriedades.
   * Especifica várias credenciais de servidor de licença ou de transporte após a renovação das credenciais.

      As credenciais antigas são mantidas no servidor para que os usuários possam continuar a exibir o conteúdo existente sem precisar reempacotar.
   * Restringe as versões de DRM/Runtime que têm permissão para fazer solicitações a um servidor de licença.
   * Define as preferências do windback do relógio do cliente.
   * Restringe a diferença de tempo permitida entre o horário da solicitação e o horário do servidor para impedir ataques de repetição.
   * Gerencia solicitações de clientes do FMRMS 1.x

      Por exemplo, o cliente FMRMS 1.x é acionado para atualizar para o Primetime DRM 2.0 ou posterior.
   * Converte metadados FMRMS 1.x em metadados DRM do Primetime sob demanda usando informações de licença do FMRMS 1.x armazenadas em um banco de dados.
   * Converte políticas FMRMS 1.x em políticas DRM do Primetime para código de amostra.
   * Importa informações de licença do FMRMS 1.x de um banco de dados existente para scripts de exemplo.
   * Obtém a versão do servidor
   * Registro de domínio
   * Cancelamento de registro de domínio
   * Solicitações de sincronização
   * Devolução de licença

* **O servidor DRM do Primetime para transmissão protegida** - É um binário pronto para uso que você pode implementar rapidamente com o mínimo esforço. É uma boa opção para clientes que desejam mostrar rapidamente a Prova de conceito ou ela *poderia* ser uma opção de produção se as necessidades de DRM personalizadas forem mínimas. Para obter mais informações, consulte Informações relacionadas abaixo.

* **O serviço DRM da Primetime Cloud** - Este é um servidor de licença hospedado em Adobe que você pode usar para o serviço de licença. (Você deve ser um licenciado do Primetime para usar este serviço.) Esse serviço em nuvem Adobe libera você das despesas, da manutenção e da engenharia necessárias para criar seu próprio serviço. Para obter mais informações, consulte Informações relacionadas abaixo.
