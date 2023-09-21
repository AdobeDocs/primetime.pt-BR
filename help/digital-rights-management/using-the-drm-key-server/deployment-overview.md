---
title: Visão geral da implantação do servidor de chaves DRM do Primetime
description: Visão geral da implantação do servidor de chaves DRM do Primetime
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# Implantar o servidor de chaves DRM do Primetime {#deploy-the-primetime-drm-key-server}

Antes de implantar o servidor de chaves DRM do Primetime, verifique se você instalou as versões necessárias do Java e do Tomcat. Consulte [Requisitos do servidor da chave DRM](../../digital-rights-management/using-the-drm-key-server/requirements.md).

O download do servidor de chaves DRM Primetime inclui [!DNL faxsks.war]. Para implantar esse arquivo WAR, copie o arquivo no do Tomcat [!DNL webapps] diretório. Se você tiver implantado anteriormente o arquivo WAR, talvez seja necessário excluir manualmente o diretório WAR desempacotado, [!DNL faxsks] no do Tomcat [!DNL webapps] diretório). Para evitar que o Tomcat descompacte arquivos WAR, edite o [!DNL server.xml] arquivo no do Tomcat [!DNL conf] e defina o `unpackWARs` atributo para `false`.

O Servidor de chaves DRM do Primetime usa opcionalmente uma biblioteca específica da plataforma (`jsafe.dll` no Windows ou `libjsafe.so` no Linux) para melhorar o desempenho. Copie a biblioteca apropriada para sua plataforma do `thirdparty/cryptoj/platform` para um local especificado pelo `PATH` variável de ambiente (ou `LD_LIBRARY_PATH` no Linux).

>[!NOTE]
>
>A versão de 64 bits do [!DNL jsafe] A biblioteca só deve ser usada se o sistema operacional e o JDK oferecerem suporte a 64 bits; caso contrário, use a versão de 32 bits.

## Configuração do SSL {#ssl-configuration}

O SSL é necessário para a entrega remota de chaves HTTPS. As conexões SSL podem ser tratadas pelo servidor de aplicativos (ou seja, configurando o SSL no Tomcat) ou podem ser tratadas em outro servidor (ou seja, um balanceador de carga, acelerador SSL ou Apache). A entrega remota da chave HTTPS requer uma conexão SSL. O servidor precisa de um certificado SSL emitido por uma CA confiável.

Há várias opções para configurar o SSL. Abaixo estão exemplos para configurar o SSL com autenticação de cliente no Apache e Tomcat.

O exemplo a seguir mostra a configuração do Apache SSL:

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

O exemplo a seguir mostra a configuração SSL do Tomcat. Para gerar arquivos de chave e certificado:

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

Quando solicitado a fornecer o nome comum, use o Nome de domínio totalmente qualificado (FQDN) do servidor.

Copiar [!DNL server.cer], e [!DNL server.key] para o diretório do Tomcat. Especifique o seguinte conector em [!DNL conf/server.xml]:

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

Você tem a opção de definir as duas propriedades do sistema Java a seguir para modificar o local da configuração e os arquivos de log do servidor de chaves DRM Primetime:

* `KeyServer.ConfigRoot` - Esse diretório contém todos os arquivos de configuração do Servidor de Chaves DRM do Primetime. Para obter detalhes sobre o conteúdo desses arquivos, consulte [Arquivos de configuração do servidor de chaves](#key-server-configuration-files). Se não estiver definido, o padrão será [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot` - Este é um diretório de log que contém os logs de aplicativo do Servidor de Chaves do iOS. Se não estiver definido, o padrão será o mesmo que `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot` - Este é um diretório de log que contém os logs de aplicativo do Servidor de Chaves Xbox. Se não estiver definido, o padrão será o mesmo que `KeyServer.ConfigRoot`.

Se você estiver usando [!DNL catalina.bat] ou [!DNL catalina.sh] para iniciar o Tomcat, essas propriedades do sistema podem ser facilmente definidas usando o `JAVA_OPTS` variável de ambiente. Quaisquer opções de Java definidas aqui serão usadas quando o Tomcat for iniciado. Por exemplo, defina:

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Credenciais de DRM do Primetime {#primetime-drm-credentials}

Para processar solicitações de chaves de clientes do Primetime DRM iOS e do Xbox 360, o Servidor de Chaves DRM do Primetime deve ser configurado com um conjunto de credenciais emitidas pelo Adobe. Essas credenciais podem ser armazenadas no PKCS#12 ( [!DNL .pfx]) ou em um HSM.

A variável [!DNL .pfx] os arquivos podem ser localizados em qualquer lugar, mas, para facilitar a configuração, a Adobe recomenda colocar o [!DNL .pfx] arquivos no diretório de configuração do locatário. Para obter mais informações, consulte [Arquivos de configuração do servidor de chaves](#key-server-configuration-files).

### Configuração de HSM {#section_13A19E3E32934C5FA00AEF621F369877}

Se optar por usar um HSM para armazenar suas credenciais de servidor, você deverá carregar as chaves privadas e os certificados no HSM e criar um *pkcs11.cfg* arquivo de configuração. Esse arquivo deve estar localizado no *KeyServer.ConfigRoot* diretório. Consulte a `<Primetime DRM Key Server>/configs` para um exemplo de arquivo de configuração PKCS 11. Para obter informações sobre o formato de [!DNL pkcs11.cfg], consulte a documentação do provedor Sun PKCS11.

Para verificar se os arquivos de configuração HSM e Sun PKCS11 estão configurados corretamente, você pode usar o seguinte comando no diretório em que o [!DNL pkcs11.cfg] o arquivo está localizado ( [!DNL keytool] O é instalado com o Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se você vir suas credenciais na lista, o HSM é configurado corretamente e o Servidor de chaves poderá acessar as credenciais.

## Arquivos de configuração do servidor de chaves {#key-server-configuration-files}

O servidor de chaves DRM do Primetime requer dois tipos de arquivos de configuração:

* Um arquivo de configuração global, [!DNL flashaccess-keyserver-global.xml]
* Um arquivo de configuração de locatário para cada locatário, [!DNL flashaccess-keyserver-tenant.xml]

Se forem feitas alterações nos arquivos de configuração, o servidor deverá ser reiniciado para que as alterações entrem em vigor.

Para evitar a disponibilização de senhas em texto não criptografado nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e de locatário devem ser criptografadas. Para obter mais informações sobre criptografia de senhas, consulte [*Scrambler de senhas* in *Uso do servidor DRM Primetime para transmissão protegida*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

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

A variável [!DNL flashaccess-keyserver-global.xml] O arquivo de configuração contém configurações que se aplicam a todos os locatários do Servidor de chaves. Este arquivo deve estar localizado em `KeyServer.ConfigRoot`. Consulte a [!DNL configs] para um exemplo de arquivo de configuração global. O arquivo de configuração global inclui o seguinte:

* Registro - Especifica o nível de registro e a frequência com que os arquivos de registro são acumulados.
* Senha HSM - Necessária somente se um HSM for usado para armazenar credenciais do servidor.

Consulte os comentários no arquivo de configuração global de exemplo localizado em `<Primetime DRM Key Server>/configs` para obter mais detalhes.

## Arquivos de configuração de locatário {#tenant-configuration-files}

A variável [!DNL flashaccess-ioskeyserver-tenant.xml] e [!DNL flashaccess-xboxkeyserver-tenant.xml] Os arquivos de configuração contêm configurações que se aplicam a um locatário específico do Servidor de Chaves DRM do Primetime. Cada locatário tem sua própria instância desses arquivos de configuração localizados em [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. Consulte a [!DNL configs/faxsks/tenants/sampletenant] diretório para um exemplo de arquivo de configuração de locatário.

Você pode especificar todos os caminhos de arquivo no arquivo de configuração do locatário como caminhos absolutos ou caminhos relativos ao diretório de configuração do locatário ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

Todos os arquivos de configuração de locatário incluem:

* Credenciais do Servidor de Chaves - Especifica uma ou mais credenciais do Servidor de Chaves (certificado e chave privada) emitidas pelo Adobe. Pode ser especificado como um caminho para um [!DNL .pfx] arquivo e uma senha ou um alias para uma credencial armazenada em um HSM. Várias dessas credenciais podem ser especificadas aqui, como caminhos de arquivo, aliases de chave ou ambos.

A variável **iOS** o arquivo de configuração do locatário inclui:

* Janela de entrega de chave - (opcional) especifica a janela de validade do carimbo de data e hora da solicitação de entrega de chave (em segundos). O valor padrão é de 500 segundos.

A variável **Xbox 360** o arquivo de configuração do locatário inclui:

* Credencial XSTS - especifica a credencial do desenvolvedor de aplicativos usada para descriptografar tokens XSTS
* Certificado de assinatura XSTS - especifica o certificado usado para verificar a assinatura em tokens XSTS.
* Lista de permissões do empacotador - certificados do empacotador confiáveis pelo servidor de chaves. Se não houver certificados do empacotador na lista, todos os certificados do empacotador serão confiáveis.

## Arquivos de log {#log-files}

Os arquivos de log gerados pelo aplicativo do Servidor de Chaves DRM Primetime ( [!DNL flashaccess-ioskeyserver_*.log] e [!DNL flashaccess-xboxkeyserver_*.log]) estará localizado no diretório especificado por `KeyServer.LogRoot`.

Os arquivos de log são diferenciados por tipo de cliente. Há dois logs por tipo de cliente:

* Um *log de acesso* - Monitora somente solicitações e respostas.
* A *log de contexto* - Contém mensagens de erro detalhadas e rastreamentos de pilha.

## Iniciando o servidor de chaves {#starting-the-key-server}

Para iniciar o servidor de chaves, inicie o Tomcat.
