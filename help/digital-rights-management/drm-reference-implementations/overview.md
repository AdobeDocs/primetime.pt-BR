---
description: nulo
seo-description: nulo
seo-title: Sobre as implementações de referência
title: Sobre as implementações de referência
uuid: f08fdb4b-aaa8-4871-bb62-1a21d5abdd8d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Sobre as implementações de referência{#about-the-reference-implementations}

Este guia descreve a instalação, configuração e operação das implementações de referência do Adobe Primetime DRM.

>[!NOTE]
>
>O Primetime DRM era anteriormente chamado de Adobe Access e antes disso, Flash Access.

As implementações de referência de DRM do Primetime incluem estes componentes:

* **Ferramentas** de linha de comando - Essas ferramentas se baseiam no mesmo código SDK do Primetime DRM usado no servidor de licenças do Primetime DRM. Você pode realizar empacotamento, licenciamento e outras tarefas de DRM na linha de comando e alternar sem problemas entre as ferramentas de linha de comando e o servidor de licenças.
* **Servidor** de licenças - Um servidor de licenças totalmente funcional e personalizável (descrito abaixo como uma das opções do seu servidor de licenças).

**Opções do License Server:**

* **Implementações** de referência do DRM Primetime - O assunto deste guia, esta implementação de referência apresenta um servidor de licença do DRM robusto que mostra todos os recursos fornecidos pelo SDK do DRM Primetime. Essa implementação é fornecida com o código fonte e instruções para a criação do código. Esta implementação não se destina a ser usada como está (embora um [!DNL .war] arquivo esteja incluído e você possa implantar rapidamente). Ela é destinada principalmente como uma referência que você pode usar para criar seu próprio servidor de licenças personalizado.

   Recursos do License Server:

   * Gerencia solicitações de autenticação usando um banco de dados para validar o nome de usuário/senha.
   * Gerencia solicitações de licença e determina o tipo de licença que está sendo emitida quando o encadeamento de licença é aplicado.
   * Emite licenças para conteúdo que inclui várias políticas de DRM Primetime.
   * Emite licenças que oferecem suporte à entrega da chave remota para clientes iOS, o que requer o Primetime DRM.
   * Emite licenças que exigem pesquisa externa e recuperação da Chave de criptografia de conteúdo (CEK).
   * Pesquisa um banco de dados para determinar se um usuário está autorizado a exibir conteúdo.
   * Pesquisa as listas de atualização da política DRM do Primetime.
   * Pesquisa listas de revogação de máquinas.
   * Usa um arquivo HSM ou PKCS12 para armazenar credenciais.
   * Criptografa senhas que você especificou em um arquivo de propriedades.
   * Especifica várias credenciais de servidor de licença ou transporte após a renovação das credenciais.

      As credenciais antigas são mantidas no servidor para que os usuários possam continuar a exibir o conteúdo existente sem precisar reempacotar.
   * Restringe versões de DRM/Runtime que têm permissão para fazer solicitações em um servidor de licenças.
   * Define as preferências de retorno do relógio do cliente.
   * Restringe a diferença de tempo permitida entre o tempo de solicitação e o tempo do servidor para evitar ataques de repetição.
   * Gerencia solicitações de clientes FMRMS 1.x

      Por exemplo, o cliente FMRMS 1.x é acionado para atualizar para o Primetime DRM 2.0 ou posterior.
   * Converte metadados FMRMS 1.x em metadados DRM Primetime sob demanda usando informações de licença FMRMS 1.x armazenadas em um banco de dados.
   * Converte políticas FMRMS 1.x em políticas DRM Primetime para código de amostra.
   * Importa informações de licença do FMRMS 1.x de um banco de dados existente para scripts de amostra.
   * Obtém a versão do servidor
   * Registro de domínio
   * Cancelamento de registro no domínio
   * Solicitações de sincronização
   * Devolução de licença

* **O Primetime DRM Server for Protected Streaming** - é um binário pronto para uso que pode ser implementado rapidamente com o mínimo de esforço. É uma boa opção para os clientes que desejam mostrar rapidamente a prova de conceito, ou *pode* ser uma opção de produção se suas necessidades de DRM personalizadas forem mínimas. Para obter mais informações, consulte Informações relacionadas abaixo.

* **O serviço** DRM da Primetime Cloud - é um servidor de licenças hospedado pela Adobe que você pode usar para o serviço de licenças. (Você deve ser um licenciado do Primetime para usar este serviço.) Este serviço em nuvem da Adobe libera as despesas, a manutenção e a engenharia necessárias para criar seu próprio serviço. Para obter mais informações, consulte Informações relacionadas abaixo.

