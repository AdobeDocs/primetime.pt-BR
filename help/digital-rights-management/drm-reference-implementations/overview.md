---
title: Sobre as implementações de referência
description: Sobre as implementações de referência
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Sobre as implementações de referência{#about-the-reference-implementations}

Este guia descreve a instalação, a configuração e a operação das implementações de referência do Adobe Primetime DRM.

>[!NOTE]
>
>O DRM do Primetime era anteriormente chamado de Adobe Access e, antes disso, Flash Access.

As implementações de referência de DRM do Primetime incluem estes componentes:

* **Ferramentas de linha de comando**  - Essas ferramentas são baseadas no mesmo código SDK de DRM do Primetime usado no servidor de licença de DRM do Primetime. Você pode realizar empacotamento, licenciamento e outras tarefas de DRM a partir da linha de comando e alternar facilmente entre usar as ferramentas de linha de comando e o servidor de licenças.
* **Servidor de licenças**  - Um servidor de licenças totalmente funcional e personalizável (descrito abaixo como uma das opções do seu servidor de licenças).

**Opções do License Server:**

* **Implementações de referência de DRM do Primetime**  - assunto deste guia, essa implementação de referência apresenta um servidor de licença de DRM robusto que mostra todos os recursos fornecidos pelo SDK de DRM do Primetime. Essa implementação é fornecida com o código-fonte e instruções para a criação do código. Esta implementação não se destina a ser usada como está (embora um arquivo [!DNL .war] seja incluído que você pode implantar rapidamente). Ela serve principalmente como uma referência que pode ser usada para criar seu próprio servidor de licenças personalizado.

   Recursos do License Server:

   * Gerencia solicitações de autenticação usando um banco de dados para validar o nome de usuário/senha.
   * Gerencia solicitações de licença e determina o tipo de licença que está sendo emitida quando o encadeamento de licenças é aplicado.
   * Emite licenças para conteúdo que inclui várias políticas de DRM do Primetime.
   * Emite licenças que oferecem suporte para a entrega de chaves remotas para clientes iOS, o que requer DRM do Primetime.
   * Emite licenças que exigem pesquisa externa e recuperação da Chave de criptografia de conteúdo (CEK).
   * Pesquisa um banco de dados para determinar se um usuário está autorizado a exibir conteúdo.
   * Pesquisa as listas de atualização da política de DRM do Primetime.
   * Pesquisa listas de revogação de máquina.
   * Usa um arquivo HSM ou PKCS12 para armazenar credenciais.
   * Criptografa senhas que você especificou em um arquivo de propriedades.
   * Especifica várias credenciais de servidor de licenças ou transporte após a renovação das credenciais.

      As credenciais antigas são mantidas no servidor para que os usuários possam continuar a visualizar o conteúdo existente sem precisar reempacotar.
   * Restringe as versões de DRM/Runtime que têm permissão para fazer solicitações a um servidor de licença.
   * Define as preferências de retorno do relógio do cliente.
   * Restringe a diferença de tempo permitida entre o tempo da solicitação e o tempo do servidor para impedir ataques de repetição.
   * Gerencia solicitações de clientes FMRMS 1.x

      Por exemplo, o cliente FMRMS 1.x é acionado para atualizar para o Primetime DRM 2.0 ou posterior.
   * Converte metadados FMRMS 1.x em metadados DRM do Primetime sob demanda usando informações de licença FMRMS 1.x armazenadas em um banco de dados.
   * Converte as políticas FMRMS 1.x em políticas DRM do Primetime para código de amostra.
   * Importa informações de licença do FMRMS 1.x de um banco de dados existente para scripts de amostra.
   * Obtém a versão do servidor
   * Registro de domínio
   * Cancelamento do registro de domínio
   * Solicitações de sincronização
   * Devolução de licença

* **Servidor DRM Primetime para transmissão protegida**  - Este é um binário pronto para uso que pode ser implementado rapidamente com o mínimo esforço. É uma boa opção para os clientes que desejam mostrar rapidamente a Prova de conceito, ou *pode* ser uma opção de produção se as necessidades de DRM personalizado forem mínimas. Para obter mais informações, consulte Informações relacionadas abaixo.

* **O serviço DRM da Primetime Cloud**  - é um servidor de licenças hospedado pelo Adobe que pode ser usado para o serviço de licenças. (Você deve ser um licenciado do Primetime para usar esse serviço.) Esse serviço de nuvem do Adobe libera você das despesas, manutenção e engenharia necessárias para criar seu próprio serviço. Para obter mais informações, consulte Informações relacionadas abaixo.

