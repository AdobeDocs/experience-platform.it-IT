---
title: Esempi di configurazioni
description: Scopri di più sulle configurazioni di esempio con utilizzando lo strumento di simulazione del grafico.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# Esempio di configurazioni del grafico

>[!NOTE]
>
>&quot;ID CRM&quot; è uno spazio dei nomi personalizzato. Pertanto, gli esempi seguenti richiedono di creare uno spazio dei nomi personalizzato con un nome visualizzato e un simbolo di identità di &quot;CRM ID&quot;.

Nella sezione seguente sono riportati alcuni esempi di scenari grafici che è possibile incontrare con Simulazione grafico.

## Solo ID CRM

Eventi:

* ID CRM: Tom, ECID: 111

Configurazione algoritmo:

| Priorità | Nome visualizzato | Simbolo di identità | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- | --- |
| 1 | ID CRM | ID CRM | CROSS_DEVICE | Sì |
| 2 | ECID | ECID | COOKIE | NO |

+++Seleziona per visualizzare il grafico simulato

+++

## ID CRM con e-mail con hash

In questo scenario, viene acquisito un ID del sistema di gestione delle relazioni con i clienti che rappresenta sia i dati online (evento esperienza) sia quelli offline (record profilo). Questo scenario comporta anche l’acquisizione di un’e-mail con hash, che rappresenta un altro spazio dei nomi inviato nel set di dati del record di gestione delle relazioni con i clienti insieme all’ID del sistema di gestione delle relazioni con i clienti.

Eventi:

* ID CRM: Tom, Email_LC_SHA256: tom<span>@acme.com
* ID CRM: Tom, ECID: 111
* CRM ID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRM ID: Summer, ECID: 222

Configurazione algoritmo:

| Priorità | Nome visualizzato | Simbolo di identità | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- | --- |
| 1 | ID CRM | ID CRM | CROSS_DEVICE | Sì |
| 2 | E-mail (SHA256, in minuscolo) | Email_LC_SHA256 | E-mail | NO |
| 3 | ECID | ECID | COOKIE | NO |

+++Seleziona per visualizzare il grafico simulato

+++

## ID CRM con e-mail con hash, telefono con hash, GAID e IDFA

Eventi:

* ID CRM: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* ID CRM: Tom, ECID: 111
* ID CRM: Tom, ECID: 222, IDFA: A-A-A
* ID CRM: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM ID: Summer, ECID: 333
* ID CRM: Summer, ECID: 444, GAID:B-B-B

Configurazione algoritmo:

| Priorità | Nome visualizzato | Simbolo di identità | Tipo di identità | Univoco per grafico |
| ---| --- | --- | --- | --- |
| 1 | ID CRM | ID CRM | CROSS_DEVICE | Sì |
| 2 | E-mail (SHA256, in minuscolo) | Email_LC_SHA256 | E-mail | NO |
| 3 | Telefono (SHA256) | Telefono_SHA256 | Telefono | NO |
| 4 | Google Ad ID (GAID) | GAID | DISPOSITIVO | NO |
| 5 | Apple IDFA (ID per Apple) | IDFA | DISPOSITIVO | NO |
| 6 | ECID | ECID | COOKIE | NO |

+++Seleziona per visualizzare il grafico simulato

+++