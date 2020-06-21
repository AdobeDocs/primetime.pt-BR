---
seo-title: Arquivo de configuração do locatário
title: Arquivo de configuração do locatário
uuid: 6e5c82c9-b8f5-4fca-8325-a884b2c779f7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Arquivo de configuração do locatário {#tenant-configuration-file}

O arquivo de configuração flashaccess-locatário.xml contém configurações que se aplicam a um locatário específico do servidor de licenças. Cada locatário tem sua própria instância desse arquivo de configuração localizado em *LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname *. Consulte o[!DNL configs/flashaccessserver/tenants/sampletenant]diretório para obter um exemplo de arquivo de configuração do locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos ao diretório de configuração do locatário (*LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname *).

O arquivo de configuração do locatário inclui:

* **Credencial** de Transporte — Especifica uma ou mais credenciais de transporte (certificado e chave privada) emitidas pela Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte &quot;[Manuseio de atualizações](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)de certificados&quot; em *Uso do SDK do Adobe Access para Proteção de Conteúdo* para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Credencial** do License Server — Especifica uma ou mais credenciais do servidor de licenças (certificado e chave privada) emitidas pela Adobe. Pode ser especificado como um caminho para um arquivo .pfx e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos. Consulte Manuseio de atualizações de certificados em *Uso do SDK do Adobe Access para Proteção de Conteúdo *para obter mais informações sobre quando credenciais adicionais são necessárias.
* **Certificados** do servidor de chaves — Opcional. Especifica o certificado do Servidor de Licenças do Servidor de Chave emitido pela Adobe. Pode ser especificado como um caminho para um arquivo .cer ou um alias para um certificado armazenado em um HSM. Essa opção deve ser especificada para que as licenças sejam emitidas para conteúdo empacotado com uma política que exija delivery de chave remota para dispositivos iOS.
* **Autorizadores** personalizados — Opcional. Especifica classes de autorizador personalizadas a serem chamadas para cada solicitação de licença. Se vários autorizadores forem especificados, eles serão chamados na ordem listada. Para obter mais informações, consulte &quot;Extensões[de autorização](../../aaxs-protected-streaming/custom-authorization-extensions.md)personalizadas&quot;.
* **Lista de embalagens autorizadas** — Opcional. Especifica certificados que identificam entidades autorizadas a disponibilizar conteúdo para este servidor de licenças. Se nenhum certificado do empacotador for especificado, o servidor emitirá licenças para conteúdo empacotado por qualquer empacotador.
* **Versão** mínima compatível do cliente (Consulte *Uso do SDK do Adobe Access para Proteção de Conteúdo*).
* **Regras de uso**

   * **Cache** de licenças — Opcional. Especifica por quanto tempo a licença pode ser armazenada no cliente. Por padrão, o cache de licenças está desativado. Para permitir o armazenamento em cache de licenças por um período limitado, defina a data de término ou o número de segundos durante os quais a licença deve ser armazenada (a partir do momento em que a licença é emitida). Definir o número de segundos como 0 desativa o armazenamento em cache de licenças.

      Observe que todas as licenças emitidas pelo Servidor para o Protected Streaming têm um período de expiração de 24 horas (86400 segundos). Portanto, esse valor se aplica implicitamente como um limite superior para qualquer data ou duração final definida para o armazenamento em cache de licenças também, com um valor máximo de 86400 segundos, mesmo que o schema imponha limites mais altos.

   * **Jogar à direita** — Deve ser especificado pelo menos um direito. Se forem especificados vários direitos, o cliente usará o primeiro direito para o qual ele atenderá a todos os requisitos.

      * **Proteção** dos resultados — Controla se a saída para dispositivos de renderização externos deve ser protegida.
      * **Restrições** de Aplicação AIR e SWF — Permitir lista opcional de aplicativos SWF e AIR que podem reproduzir o conteúdo (ou seja, somente os aplicativos especificados são permitidos). Os aplicativos SWF são identificados por um URL ou pelo resumo do SWF e pelo tempo máximo para permitir o download e a verificação do resumo. Para obter informações sobre como calcular o resumo do SWF, consulte a seção &quot;Calculadora de hash do SWF&quot;. Os aplicativos AIR e iOS são identificados por uma ID do editor e ID da aplicação opcional, versão mínima e versão máxima. Se nenhuma restrição de aplicativo for especificada, qualquer aplicativo SWF ou AIR poderá reproduzir o conteúdo.
      * **Restrições** do módulo de tempo de execução e DRM — Especifica o nível mínimo de segurança necessário para o módulo DRM/Runtime. Opcionalmente, inclui uma lista de blocos de versões que não têm permissão para reproduzir o conteúdo. As versões do módulo são identificadas por atributos como sistema operacional e/ou número de versão. Restrições do módulo DRM e restrições do módulo de tempo de execução agora suportam os seguintes atributos adicionais:

         * `oemVendor`
         * `model`
         * `screenType`
         Os seguintes atributos agora são opcionais:

         * `osVersion`
         * `version`
      * **Requisitos** de capacidade do dispositivo — Especifica opcionalmente os recursos de hardware necessários para acessar o conteúdo.
      * **Requisitos** de detecção de quebra-maré — Especifica opcionalmente que a reprodução não é permitida para dispositivos nos quais a quebra de carateres é detectada.



Consulte os comentários no arquivo de configuração do locatário de exemplo para obter mais detalhes.
