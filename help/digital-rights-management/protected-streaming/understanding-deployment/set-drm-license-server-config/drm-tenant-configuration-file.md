---
description: O arquivo de configuração flashaccess-locatário.xml inclui configurações que se aplicam a um locatário específico do servidor de licenças.
seo-description: O arquivo de configuração flashaccess-locatário.xml inclui configurações que se aplicam a um locatário específico do servidor de licenças.
seo-title: Arquivo de configuração do locatário
title: Arquivo de configuração do locatário
uuid: bc9ee4a1-63b6-4362-9929-3e9fe8251075
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Arquivo de configuração do locatário{#tenant-configuration-file}

O arquivo de configuração flashaccess-locatário.xml inclui configurações que se aplicam a um locatário específico do servidor de licenças.

Cada inquilino suporta sua própria instância deste arquivo de configuração localizado em [!DNL &lt;LicenseServer.ConfigRoot>/flashaccess server/tenants/<tenantname>]. Consulte o [!DNL configs/flashaccessserver/tenants/sampletenant] diretório para obter um exemplo de arquivo de configuração do locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou como caminhos relativos ao diretório de configuração do locatário ( [!DNL &lt;LicenseServer.ConfigRoot>/flashaccess server/tenants/<tenantname>]).

O arquivo de configuração do locatário inclui:

* *Credencial* de Transporte — Especifica uma ou mais credenciais de transporte (certificado e chave privada) emitidas pela Adobe. Pode ser especificado como um caminho para um [!DNL .pfx] arquivo e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

   Consulte *Manuseio de atualizações* de certificados em *Uso do SDK do Adobe Primetime DRM para Proteção de Conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.

* *Credencial* do License Server — Especifica uma ou mais credenciais do servidor de licenças (certificado e chave privada) que a Adobe emitiu. Você pode especificar as credenciais do servidor de licenças como um caminho para um [!DNL .pfx] arquivo e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

   Consulte *Manuseio de atualizações* de certificados em *Uso do SDK do Adobe Primetime DRM para Proteção de Conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.

* *Certificados* do servidor de chaves — Especifica opcionalmente o certificado do Servidor de Licenças do Servidor de Chave que a Adobe emitiu. Você pode especificar o certificado do servidor de licenças do servidor de chaves como um caminho para um [!DNL .cer] arquivo ou um alias para um certificado armazenado em um HSM. Essa opção deve ser especificada para emitir licenças para conteúdo que é empacotado com uma política de DRM que requer delivery de chave remota para dispositivos iOS.

* *Autorizadores* personalizados — Especifica opcionalmente classes de autorizador personalizadas para chamar para cada solicitação de licença. Se vários autorizadores forem especificados, eles serão chamados na ordem listada.
* *Lista de embalagens autorizadas* — Especifica, opcionalmente, certificados que identificam entidades autorizadas a disponibilizar conteúdo para este servidor de licenças. Se nenhum certificado do empacotador for especificado, o servidor emitirá licenças para o conteúdo empacotado por qualquer empacotador. Se o servidor receber uma solicitação de licença de um empacotador não autorizado, a solicitação será negada.
* *Versão* mínima compatível do cliente Consulte Uso do SDK do Adobe Primetime DRM para proteção de conteúdo.

* *Regras de uso*

   * *Cache* de licenças — Especifica opcionalmente quanto tempo você pode armazenar a licença no cliente. Por padrão, o cache de licenças está desativado. Se quiser ativar o armazenamento em cache de licenças por um período limitado, é necessário definir a data de término ou o número de segundos durante os quais a licença deve ser armazenada (a partir do momento em que a licença é emitida). Definir o número de segundos como 0 desativa o armazenamento em cache de licenças.

      >[!NOTE]
      >
      >Todas as licenças emitidas pelo Servidor para Transmissão Protegida incluem um período de expiração de 24 horas (86400 segundos). Esse valor se aplica implicitamente como um limite superior para qualquer data ou duração final definida para o armazenamento em cache de licenças também, com um valor máximo de 86400 segundos, mesmo que o schema imponha limites mais altos.

   * *Jogar à direita* — Deve ser especificado um mínimo de um direito. Se você especificar vários direitos, o cliente usará o primeiro direito que atender a todos os requisitos.

      * *Proteção* dos resultados — Controla se a saída para dispositivos de renderização externos deve ser protegida.
      * *Restrições* de Aplicação AIR e SWF — Permitir lista opcional de aplicativos SWF e AIR que podem reproduzir o conteúdo (por exemplo, somente os aplicativos especificados são permitidos). Os aplicativos SWF são identificados por um URL ou pelo resumo do SWF e pelo tempo máximo para permitir o download e a verificação do resumo.

         Consulte Calculadora *de hash de* SWF para obter informações sobre como calcular o resumo de SWF.

         Uma ID do editor e um ID da aplicação opcional, uma versão mínima e uma versão máxima identificam aplicativos AIR e iOS. Se você não especificar nenhuma restrição de aplicativo, qualquer aplicativo SWF ou AIR poderá reproduzir o conteúdo.

      * *Restrições* do módulo de tempo de execução e DRM — Especifica o nível mínimo de segurança necessário para o módulo DRM/Runtime. Opcionalmente, inclui uma lista de blocos de versões que não têm permissão para reproduzir o conteúdo. As versões do módulo são identificadas por atributos, como o sistema operacional e/ou um número de versão.

         Restrições do módulo DRM e restrições do módulo de tempo de execução agora suportam os seguintes atributos adicionais:

         * `oemVendor`
         * `model`
         * `screenType`
         Os seguintes atributos agora são opcionais:

         * `osVersion`
         * `version`
      * *Requisitos* de capacidade do dispositivo — Especifica opcionalmente os recursos de hardware necessários para acessar o conteúdo.
      * *Requisitos* de detecção de quebra-maré — Especifica opcionalmente que a reprodução não é permitida para dispositivos nos quais a quebra de carateres é detectada.



Consulte os comentários no arquivo de configuração do locatário de exemplo para obter mais detalhes.
