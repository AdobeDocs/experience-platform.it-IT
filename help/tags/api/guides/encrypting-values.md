---
title: Crittografia dei valori
description: Scopri come crittografare i valori sensibili quando si utilizzano l’API di Reactor.
exl-id: d89e7f43-3bdb-40a5-a302-bad6fd1f4596
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 100%

---

# Crittografia dei valori

Quando si utilizzano i tag in Adobe Experience Platform, alcuni flussi di lavoro richiedono valori sensibili (ad esempio, una chiave privata per la distribuzione delle librerie agli ambienti tramite host). Il carattere sensibile di tali credenziali richiede
trasferimento e archiviazione sicuri.

Questo documento descrive come crittografare i valori sensibili utilizzando la [crittografia GnuPG](https://www.gnupg.org/gph/en/manual/x110.html) (nota anche come GPG) in modo che solo il sistema di tag possa leggerli.

## Ottenere la chiave GPG pubblica e il checksum

Dopo il [download](https://gnupg.org/download/) e l’installazione dell’ultima versione di GPG, devi ottenere la chiave GPG pubblica per l’ambiente di produzione dei tag:

* [Chiave GPG](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg)
* [Checksum](https://github.com/adobe/reactor-developer-docs/blob/master/files/launch%40adobe.com_pub.gpg.sum)

## Importare la chiave portachiavi

Una volta salvata la chiave nel computer, il passo successivo è quello di aggiungerla al portachiavi GPG.

**Sintassi**

```shell
gpg --import {KEY_NAME}
```

| Parametro | Descrizione |
| --- | --- |
| `{KEY_NAME}` | Nome del file della chiave pubblica. |

{style="table-layout:auto"}

**Esempio**

```shell
gpg --import launch@adobe.com_pub.gpg
```

## Crittografare i valori

Dopo aver aggiunto la chiave al portachiavi, puoi iniziare a crittografare i valori utilizzando il flag `--encrypt`. Lo script seguente illustra il funzionamento di questo comando:

```shell
echo -n 'Example value' | gpg --armor --encrypt -r "Tags Data Encryption <launch@adobe.com>"
```

Questo comando può essere suddiviso come segue:

* L’input viene fornito al comando `gpg`.
* `--armor` crea un output in formato ASCII anziché binario. Questo semplifica il trasferimento del valore tramite JSON.
* `--encrypt` incarica GPG di crittografare i dati.
* `-r` imposta il destinatario dei dati. Solo il destinatario (il detentore della chiave privata che corrisponde alla chiave pubblica) può decrittografare i dati. Per trovare nome del destinatario della chiave desiderata, si può esaminare l’output di `gpg --list-keys`.

Il comando precedente utilizza la chiave pubblica per `Tags Data Encryption <launch@adobe.com>` per crittografare il valore, `Example value`, in formato ASCII blindato.

L’output del comando sarà simile al seguente:

```shell
-----BEGIN PGP MESSAGE-----

hQIMAxJHCI6fydT/ARAAwQ0Y0k7eSAbd0T9seoaWX75G70O2gxAF20KY5FWiZ9/m
/RkgJwhJusZyEdazC/CmAdfXi9bsVxQT0i06ErUxXfQF0VtweRlcyRBsxzLz6Hr+
BpYGnq+cCCzGAT73Gg1CM4UWmaPKLLyWKGkXtDBAqVBRAIQT/8JhnkbyWIohHkWV
I/Uf7NrPXuaSmrqZ1SZQgwjIM3qNMR02qtqg59dncKoCQBji8Oeb8lqRLskRT0Jq
gVgbJYwSe2n6KpJkELJ6QtF9lCRl1+yU4mvM4jBHgkM1+vb1WmbFRIR40dDpg85N
0J9hVj4bg//eLRDfAdEC9kgq9Atph0WqJ5EpehdS7yVO9lO8mpbpqZ4BCGjTi/VS
isEPr6eZ2mxRbk8f9Z4csRZnkErY8ep5+cqC5CZVdmguWvC9PKzXqEsPFd0PSYk3
Qp3UIW2/JMf16E5CKmntm+gKdl6kggZOOvNQuyJYa9yNbzySPerHXsknTOxV+QP/
WXwrAL52g5+gpMib7Ve/KBz5/OViDhDqkmHzlGad73W74d+CYjf0AnuXuWRRlUMT
s8ORw1eplInldhXk2mgkGPZS/gWDs3zpKUu4GSO9AaeWldynLG/Bgh78XhumQ58h
ekGD+p3PyyvxjfS5G/wf9HQZ085+mnjpKFa7fuFBQPbg4WpBadhWrhobthC+hN3S
SAE9yWU11Y3xpoxqg4y7iYZ6rnX+qP2oUNYxC2/hdhsFbbZtUh4s51qaoLbe0iWB
OUoIPf4KxTaboHZOEy32ZBng5heVrn4i9w==
=jrfE
-----END PGP MESSAGE-----
```

Questo output può essere decrittografato solo da sistemi che dispongono
di una chiave privata che corrisponde alla chiave pubblica `Tags Data Encryption <launch@adobe.com>`.

Questo output è il valore che deve essere fornito quando si inviano dati all’API di Reactor. Il sistema memorizza questo output crittografato e lo decrittografa temporaneamente in base alle necessità. Ad esempio, il sistema decrittografa le credenziali host abbastanza a lungo per avviare una connessione al server e quindi rimuove immediatamente ogni traccia del valore decrittografato.

>[!NOTE]
>
>Il formato del valore crittografato e blindato è importante. Assicurati che eventuali a-capo siano correttamente preceduti da un carattere di escape, all’interno del valore specificato nella richiesta.
