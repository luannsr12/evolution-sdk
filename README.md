
# SDK PHP para Evolution API WhatsApp

[![Packagist](https://img.shields.io/packagist/v/luannsr12/apiwpp.svg?style=flat)](https://packagist.org/packages/luannsr12/apiwpp)
[![License](https://img.shields.io/packagist/l/luannsr12/apiwpp.svg?style=flat)](LICENSE)
[![Downloads](https://img.shields.io/packagist/dt/luannsr12/apiwpp.svg?style=flat)](https://packagist.org/packages/luannsr12/apiwpp)
[![PHP Version](https://img.shields.io/packagist/php-v/luannsr12/apiwpp.svg?style=flat)](https://www.php.net/)

## Introdução

`apiwpp` é uma SDK em PHP para integração com a Evolution API, possibilitando o envio de mensagens, gerenciamento de dispositivos (instâncias) e configuração de webhooks no WhatsApp de forma simples e eficiente.

---

## Requisitos

- PHP >= 8.2
- Composer  
- Servidor Evolution API >= v2.0 configurado e acessível  

---

## Instalação

```bash
composer require luannsr12/apiwpp
```

---

## Configuração Inicial

```php
use Apiwpp\Config\Api;

Api::setConfigs('SEU_TOKEN_ADMIN', 'URL_DA_SUA_API');
Api::debug(true); // Ativa o modo debug (opcional)
```

---

## Gerenciamento de Devices (Instâncias)

### Criar nova instância

```php
use Apiwpp\Api\Evolution2\Device;

$response = Device::create('TOKEN_DA_INSTANCIA', 'NOME_DA_INSTANCIA');
print_r($response);
```

### Definir instância ativa para envio

```php
Device::setInstance('TOKEN_INSTANCIA', 'NOME_INSTANCIA');
```

---

## Envio de Mensagens

### Mensagem de texto simples

```php
use Apiwpp\Api\Evolution2\Message;

Message::type('text');
Message::phone('551199999999');
Message::text('Olá, esta é uma mensagem de teste.');

if (Message::send()) {
    echo 'Mensagem enviada com sucesso!';
} else {
    echo 'Falha ao enviar mensagem.';
}
```

### Enviar mídia (imagem, áudio, vídeo, documento)

```php
Message::type('image'); // audio, document, video
Message::phone('551199999999');
Message::file('https://link-da-imagem-ou-caminho-local.jpg');
Message::caption('Legenda da imagem'); // opcional

Message::send();
```

---

## Verificação de Número no WhatsApp

```php
use Apiwpp\Api\Evolution2\Number;

Number::phone('551199999999');

if (Number::check()) {
    echo 'Número existe no WhatsApp.';
} else {
    echo 'Número não encontrado.';
}
```

---

## Webhooks

### Configurar URL para recebimento de mensagens

```php
use Apiwpp\Api\Evolution2\Webhook;

Webhook::setUrl('https://seusite.com.br/webhook');
Webhook::enable(true);
```

---

## Tratamento de Erros

```php
use Apiwpp\Error\ExceptionError;

try {
    // Código da SDK
} catch (Exception $e) {
    echo ExceptionError::getMessage();
}
```

---

## Exemplos

No diretório `/examples` você encontra scripts prontos para:

- Criar e conectar instância  
- Enviar mensagens simples e mídia  
- Verificar número WhatsApp  
- Configurar webhooks  

---

## Contribuições

Bug reports, sugestões e pull requests são bem-vindos!  
Por favor, abra issues no GitHub para discussão.

---

## Licença

MIT License © Luan Alves

---

## Contato

Para dúvidas ou suporte: luanalvesnsr@gmail.com
