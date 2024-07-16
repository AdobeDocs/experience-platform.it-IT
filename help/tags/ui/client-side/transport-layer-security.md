---
title: Informazioni su Transport Layer Security (TLS)
description: Informazioni sulle versioni e le crittografie TLS utilizzate
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 16%

---

# Informazioni su Transport Layer Security (TLS)

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Per un riferimento consolidato delle modifiche terminologiche, consulta il documento [aggiornamenti dei termini](../../term-updates.md).

Transport Layer Security (TLS) è un protocollo di crittografia che fornisce sicurezza end-to-end per i dati inviati tra le applicazioni tramite Internet. Per informazioni più dettagliate su TLS, consulta la documentazione [Nozioni di base su TLS](https://www.internetsociety.org/deploy360/tls/basics/).

I tag in Adobe Experience Platform sono un sistema di gestione dei tag progettato per caricare dinamicamente gli script sul sito web. TLS protegge la comunicazione tra l&#39;host Adobe `assets.adobedtm.com` e il sito Web quando questi script vengono caricati.

Sono disponibili più versioni di TLS e supporta un certo numero di crittografie diverse. Non tutte le versioni e le crittografie sono uguali, in quanto alcune sono considerate meno o più sicure di altre.

## Versioni e cifrature TLS supportate

L’opzione host di Adobe supporta attualmente le seguenti versioni e crittografie TLS:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Hosting autonomo

Se sei [self-hosting](../publishing/hosts/self-hosting-libraries.md) della tua libreria, le versioni di TLS supportate saranno determinate dal tuo servizio di hosting.

## Puntatori TLS da rimuovere il 1° maggio 2024

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```
