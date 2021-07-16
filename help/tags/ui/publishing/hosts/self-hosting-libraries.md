---
title: Self-hosting delle librerie
description: Scopri come implementare l’hosting autonomo per le build della libreria di tag in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 74%

---

# Self-hosting delle librerie

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

I tag in Adobe Experience Platform consentono la produzione di un set di file denominato [build](../builds.md). Questo insieme di file controlla il comportamento dell&#39;applicazione in fase di esecuzione.

Le build devono essere ospitate in un punto in modo da consentire ai dispositivi client di recuperarle in fase di esecuzione, in base alle esigenze.

Platform può gestire l’hosting di questi file oppure puoi farlo autonomamente.

## Gestito da Adobe {#managed-by-adobe}

Adobe non opera nel settore del hosting web. Se scegli l&#39;hosting gestito da Adobe, le build vengono distribuite a una rete di distribuzione di contenuti (CDN) di terze parti con la quale abbiamo stipulato un contratto.

Attualmente, il provider CDN principale è Akamai. I file in hosting su Akamai hanno un dominio `assets.adobedtm.com`.

### Perché utilizzare l&#39;hosting gestito?

Il motivo principale per utilizzare l&#39;hosting gestito è la comodità. Creare l&#39;host richiesto è più semplice e non dovrai preoccuparti della manutenzione.

## Hosting autonomo

Se non desideri che Adobe gestisca i file ospitati, devi ospitarli personalmente. Per ospitare i file, devi ottenere le build completate da Platform ed essere responsabile di ottenere i file tramite il ciclo di rilascio aziendale sui server gestiti dall’azienda.

### Perché utilizzare l&#39;hosting autonomo?

Esistono diversi motivi per scegliere di ospitare i propri file di build.

* Alcuni browser bloccano il dominio assets.adobedtm.com in base alle impostazioni della privacy configurate dall&#39;utente finale
* L&#39;hosting autonomo riduce il numero richiesto di ricerche DNS
* È necessario utilizzare HTTP/2
* Disponi di intestazioni specifiche da impostare per la sicurezza
* I requisiti di controllo della cache differiscono dalle impostazioni predefinite Adobi
* Un maggiore controllo sulla posizione dei nodi Edge
* La tua organizzazione dispone di requisiti di sicurezza e legali che impediscono l&#39;utilizzo dell&#39;opzione gestita da Adobe

### Come eseguire l&#39;hosting automatico.

Esistono due metodi per acquisire le build completate, in modo da poter eseguire l&#39;hosting automatico.

* Scarica
* Consegna diretta

#### Scarica

Le build possono essere distribuite come file .zip in pacchetto (crittografia facoltativa). Puoi quindi decomprimere il pacchetto e inserirlo nel processo di rilascio per inserirlo nei server.

Utilizza un host [gestito da Adobe](self-hosting-libraries.md) e seleziona l&#39;opzione [Archivia](../environments.md) nell&#39;ambiente. L&#39;ambiente fornisce un collegamento per il download. Ogni volta che crei una build, puoi recuperarla dal collegamento del download fornito.

#### Consegna diretta

Puoi anche distribuire le build direttamente a un server SFTP creato. Ti assumi la responsabilità di inserire questi elementi nel tuo ciclo di rilascio e di eseguire il push in tempo reale.

Per eseguire una consegna diretta, è necessario creare un [host SFTP](sftp-host.md) e assegnare tale host all&#39;ambiente. Ogni volta che crei una libreria in tale ambiente, i file vengono consegnati al server SFTP.
