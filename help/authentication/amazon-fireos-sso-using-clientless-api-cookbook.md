---
title: Amazon FireOS SSO usando o guia da API sem cliente
description: Amazon FireOS SSO usando o guia da API sem cliente
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS SSO usando o guia da API sem cliente {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

## Introdução {#Introduction}

Este documento fornece instruções para implementar a versão SSO do Amazon do fluxo de Autenticação do Adobe Primetime usando a API sem cliente. A primeira parte deste documento foca na especificidade da versão Amazon da arquitetura, para os muitos parceiros já familiarizados e experientes com a implementação.

A segunda parte do documento passa pelas etapas principais para implementar a API sem cliente de Autenticação Adobe Primetime.

Para obter uma visão geral técnica de como a solução sem cliente funciona, consulte a [Visão geral da REST API](/help/authentication/rest-api-overview.md). O Adobe é o contato preferido para oferecer suporte sobre a arquitetura geral e as primeiras implementações.

## Amazon Client SSO {#AMZ-Clientless-SSO}

### Arquitetura de alto nível {#High-Level-Arch}

A implementação de SSO sem cliente do Amazon é simples e quase idêntica às APIs sem cliente comuns da Autenticação Adobe Primetime.

Você precisará usar o SDK do Amazon para recuperar uma carga personalizada e usá-la ao chamar APIs sem cliente do Adobe.

Se a carga for reconhecida e corresponder a uma sessão autenticada, as APIs sem cliente retornarão imediatamente com o token da sessão.

### Como criar o aplicativo para usar o Amazon SDK {#Build-entries}

* Baixe e copie a versão mais recente [SDK do Stub do Amazon](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) em uma pasta /SSOEnabler paralela ao diretório do aplicativo
* Atualize arquivos de manifesto/gradle para usar a biblioteca :

   **Adicione a seguinte linha ao arquivo Manifest :**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Entradas do arquivo de grade:**

   Em repositórios:

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   Em dependências, adicione:

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* Lidando com a ausência do aplicativo complementar do Amazon:

   Embora não seja provável que o companheiro não esteja presente no dispositivo Amazon em que seu aplicativo está em execução, você deve encontrar um ClassNotFoundException no tempo de execução na seguinte classe: `com.amazon.ottssotokenlib.SSOEnabler`.

   Se isso acontecer, tudo o que você precisa fazer é ignorar a etapa de carga e voltar para o fluxo regular do PrimeTime. O SSO não será ativado, mas o fluxo de autenticação regular ocorrerá normalmente.

</br>

### Como obter a carga SSO do Amazon usando o Amazon SDK {#UseAmazonSSO}

Durante a inicialização do aplicativo, obtenha uma instância do SSOEnabler. Com base na arquitetura de seu aplicativo, você deve decidir entre uma implementação síncrona ou assíncrona.

Se, por qualquer motivo, as chamadas de API não retornarem uma carga útil, use o fluxo não-SSO regular e entre em contato com seus parceiros Amazon e Adobe para investigar.

**API assíncrona**

* Obter instância do SSO Enabler:

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* Definir o retorno de chamada 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * O pacote de resposta bem-sucedido conterá:
      * Token SSO como uma string com chave &quot;SSOToken&quot;
   * O pacote de resposta da falha conterá:
      * código de erro como um int com chave &quot;ErrorCode&quot;
      * descrição do erro como uma string com chave &quot;ErrorDescription&quot;


* Obter token SSO

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* Essa API fornecerá a resposta via callback definido durante a inicialização.

   **Ex**. chamada usando a instância singleton criada durante a inicialização:

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**APIs síncronas**

* Obtenha a instância do SSO Enabler e defina o retorno de chamada

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* Obter token SSO

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * Essa API bloqueará o encadeamento do chamador e responderá com o pacote de resultados. Como esta é uma chamada síncrona, não use-a no seu thread principal.

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * Valor em milissegundos. se definido, substitua o valor padrão de tempo limite de 1 minuto para a API de sincronização.



### Atualização da API sem cliente do Adobe Primetime para usar o Registro dinâmico de clientes {#clientlessdcr}

Se esta for a sua primeira implementação, consulte o **Visão geral técnica sem cliente** e entre em contato com o Adobe caso precise de suporte.

A API sem cliente do Adobe requer que os aplicativos usem o Registro dinâmico de clientes para fazer chamadas para servidores Adobe.

* Para usar o Registro dinâmico de clientes em seu aplicativo, siga as instruções em [ Dynamic Client Registration Management para registrar o aplicativo](/help/authentication/dynamic-client-registration-management.md).

* Para implementar a API Dynamic Client Registration para executar solicitações de autenticação e autorização para servidores da Adobe Primetime, siga as instruções em [API dinâmica de registro de cliente](/help/authentication/dynamic-client-registration-api.md) .

### Atualização da API sem cliente do Adobe Primetime para usar o Amazon SSO {#clientlesssso}

A carga SSO do Amazon obtida do SDK do Amazon precisa estar presente nas solicitações feitas nos endpoints de Autenticação do Adobe Primetime :

```
      /adobe-services/*
      /reggie/*
      /api/*
```


Todos os endpoints de Autenticação do Primetime oferecem suporte aos seguintes métodos para receber o identificador do escopo do dispositivo ou o identificador do escopo da plataforma (presente na carga útil SSO do Amazon):

* Como um cabeçalho : &quot;Adobe-Subject-Token&quot;
* Como parâmetro de consulta : &quot;ast&quot;
* Como um parâmetro de publicação : &quot;ast&quot;


>[!NOTE]
>
>Se o identificador do escopo do dispositivo ou o identificador do escopo da plataforma for enviado como parâmetro de consulta/postagem, ele deverá ser incluído ao gerar a assinatura da solicitação.

>[!NOTE]
>
>Usando o parâmetro de consulta &quot;ast&quot;, todo o url pode se tornar muito longo e rejeitado. Na chamada /autentica, esse parâmetro pode ser ignorado, pois foi fornecido na chamada /regcode

**Exemplos:**

**Enviar como cabeçalho personalizado**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**Enviar como parâmetro de consulta**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**Enviar como parâmetro de publicação**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>Se o SSO do Amazon não estiver presente ou for inválido, a Autenticação do Adobe Primetime ignorará o atributo e as chamadas serão executadas como se o SSO não estivesse presente.
