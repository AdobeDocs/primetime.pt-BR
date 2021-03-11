---
title: Implantar a visão geral do servidor de chaves DRM do Primetime
description: Implantar a visão geral do servidor de chaves DRM do Primetime
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Implantar o servidor de chaves DRM do Primetime {#deploy-the-primetime-drm-key-server}

Antes de implantar o Primetime DRM Key Server, verifique se você instalou as versões necessárias do Java e do Tomcat. Consulte [Requisitos do servidor de chaves DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

O download do Servidor de chaves DRM do Primetime inclui [!DNL faxsks.war]. Para implantar esse arquivo WAR, copie o arquivo para o diretório [!DNL webapps] do Tomcat. Se você já implantou o arquivo WAR, talvez precise excluir manualmente o diretório WAR descompactado, [!DNL faxsks] no diretório [!DNL webapps] do Tomcat). Para impedir que o Tomcat descompacte arquivos WAR, edite o arquivo [!DNL server.xml] no diretório [!DNL conf] do Tomcat e defina o atributo `unpackWARs` para `false`.

Como opção, o Primetime DRM Key Server usa uma biblioteca específica da plataforma (`jsafe.dll` no Windows ou `libjsafe.so` no Linux) para melhorar o desempenho. Copie a biblioteca apropriada para sua plataforma de `thirdparty/cryptoj/platform` para um local especificado pela variável de ambiente `PATH` (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits da biblioteca [!DNL jsafe] só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits, caso contrário, usarão a versão de 32 bits.

## Configuração SSL {#ssl-configuration}

O SSL é necessário para a entrega de chaves HTTPS remotas. As conexões SSL podem ser manipuladas pelo servidor de aplicativos (ou seja, pela configuração do SSL no Tomcat) ou em outro servidor (ou seja, um balanceador de carga, um acelerador SSL ou o Apache). A entrega remota de chaves HTTPS requer uma conexão SSL. O servidor precisa de um certificado SSL emitido por uma CA confiável.

Há uma variedade de opções para configurar o SSL. Abaixo estão exemplos para configurar o SSL com autenticação de cliente no Apache e Tomcat.

O exemplo a seguir mostra a configuração SSL do Apache:

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

O exemplo a seguir mostra a configuração SSL do Tomcat. Para gerar arquivos de certificado e chave:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando solicitado para o nome comum, use o FQDN (Nome de Domínio Totalmente Qualificado) do seu servidor.

Copie [!DNL server.cer] e [!DNL server.key] para o diretório Tomcat. Especifique o seguinte Conector em [!DNL conf/server.xml]:

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Propriedades do sistema Java {#java-system-properties}

Você tem a opção de definir as duas propriedades do sistema Java a seguir para modificar o local da configuração e dos arquivos de log do Servidor de chaves DRM do Primetime:

* `KeyServer.ConfigRoot` - Esse diretório contém todos os arquivos de configuração do Primetime DRM Key Server. Para obter detalhes sobre o conteúdo desses arquivos, consulte [Arquivos de configuração do Servidor de Chave](#key-server-configuration-files). Se não estiver definido, o padrão será [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Este é um diretório de log que contém registros de aplicativos do Servidor de Chave do iOS. Se não estiver definido, o padrão será igual a `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este é um diretório de log que contém os logs de aplicativo do Servidor de Chave Xbox. Se não estiver definido, o padrão será igual a `KeyServer.ConfigRoot`.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, essas propriedades do sistema poderão ser facilmente definidas usando a variável de ambiente `JAVA_OPTS`. Qualquer opção Java definida aqui será usada quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciais de DRM do Primetime {#primetime-drm-credentials}

Para processar as principais solicitações dos clientes Primetime DRM iOS e Xbox 360, o Primetime DRM Key Server deve ser configurado com um conjunto de credenciais emitidas pelo Adobe. Essas credenciais podem ser armazenadas em arquivos PKCS#12 ( [!DNL .pfx]) ou em um HSM.

Os arquivos [!DNL .pfx] podem ser localizados em qualquer lugar, mas para facilitar a configuração, o Adobe recomenda colocar os arquivos [!DNL .pfx] no diretório de configuração do locatário. Para obter mais informações, consulte [Arquivos de configuração do Servidor de Chave](#key-server-configuration-files).

### Configuração do HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se você optar por usar um HSM para armazenar suas credenciais de servidor, deverá carregar as chaves privadas e os certificados no HSM e criar um arquivo de configuração *pkcs11.cfg*. Este arquivo deve estar localizado no diretório *KeyServer.ConfigRoot*. Consulte o diretório `<Primetime DRM Key Server>/configs` para obter um exemplo de arquivo de configuração PKCS 11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11 .

Para verificar se os arquivos de configuração HSM e Sun PKCS11 estão configurados corretamente, você pode usar o seguinte comando do diretório em que o arquivo [!DNL pkcs11.cfg] está localizado ( [!DNL keytool] está instalado com o Java JRE e o JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente e o Servidor de chaves poderá acessar as credenciais.

## Arquivos de configuração do Servidor de Chave {#key-server-configuration-files}

O Primetime DRM Key Server requer dois tipos de arquivos de configuração:

* Um arquivo de configuração global, [!DNL flashaccess-keyserver-global.xml]
* Um arquivo de configuração de locatário para cada locatário, [!DNL flashaccess-keyserver-tenant.xml]

Se forem feitas alterações nos arquivos de configuração, o servidor deverá ser reiniciado para que as alterações entrem em vigor.

Para evitar disponibilizar senhas em texto claro nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e do locatário devem ser criptografadas. Para obter mais informações sobre como criptografar senhas, consulte [*Scrambler de senha* em *Usar o servidor DRM Primetime para transmissão protegida*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Estrutura do diretório de configuração {#configuration-directory-structure}

Os diretórios de configuração têm a seguinte estrutura:

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## Arquivo de configuração global {#global-configuration-file}

O arquivo de configuração [!DNL flashaccess-keyserver-global.xml] contém configurações que se aplicam a todos os locatários do Servidor de Chave. Este arquivo deve estar localizado em `KeyServer.ConfigRoot`. Consulte o diretório [!DNL configs] para obter um exemplo de arquivo de configuração global. O arquivo de configuração global inclui o seguinte:

* Registro - Especifica o nível de registro e a frequência com que os arquivos de log são rolados.
* Senha do HSM - Obrigatório somente se um HSM for usado para armazenar credenciais do servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado em `<Primetime DRM Key Server>/configs` para obter mais detalhes.

## Arquivos de configuração de locatário {#tenant-configuration-files}

Os arquivos de configuração [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] contêm configurações que se aplicam a um locatário específico do Servidor de chaves DRM do Primetime. Cada locatário tem sua própria instância desses arquivos de configuração localizados em [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte o diretório [!DNL configs/faxsks/tenants/sampletenant] para obter um exemplo de arquivo de configuração de locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos para o diretório de configuração do locatário ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos os arquivos de configuração do locatário incluem:

* Credenciais do Servidor de Chave - Especifica uma ou mais credenciais do Servidor de Chave (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um arquivo [!DNL .pfx] e uma senha, ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

O arquivo de configuração do locatário do **iOS** inclui:

* Janela principal de entrega - (Opcional) Especifica a janela de validade do carimbo de data e hora da solicitação de entrega-chave (em segundos). O valor padrão é de 500 segundos.

O arquivo de configuração do locatário **Xbox 360** inclui:

* Credencial XSTS - Especifica a credencial do desenvolvedor do aplicativo usada para descriptografar tokens XSTS
* Certificado de assinatura XSTS - Especifica o certificado usado para verificar a assinatura em tokens XSTS.
* Lista de permissões do Empacotador - Certificados do Empacotador que são fidedignos pelo Servidor de Chave. Se não houver certificados de empacotador contidos na lista, todos os certificados de empacotador serão confiáveis.

## Arquivos de log {#log-files}

Os arquivos de log gerados pelo aplicativo Primetime DRM Key Server ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) estarão localizados no diretório especificado por `KeyServer.LogRoot`.

Os arquivos de log são diferenciados por tipo de cliente. Há dois logs por tipo de cliente:

* Um *log de acesso* - Monitora somente solicitações e respostas.
* A *context log* - Contém mensagens de erro detalhadas e rastreamentos de pilha.

## Iniciando o Servidor de Chave {#starting-the-key-server}

Para iniciar o Servidor de chaves, inicie o Tomcat.