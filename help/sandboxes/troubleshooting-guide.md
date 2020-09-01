---
keywords: Experience Platform;home;popular topics;sandbox troubleshooting
solution: Experience Platform
title: Guida alla risoluzione dei problemi sandbox
topic: troubleshooting guide
description: Questo documento contiene le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6f4714561c2946a084eed4e89d3148df5b8044f5
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi sandbox

Questo documento contiene le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi della piattaforma, consulta la guida [alla risoluzione dei problemi del Experience Platform](../landing/troubleshooting.md).

Le sandbox suddividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali. Per ulteriori informazioni, consultate la panoramica [delle](home.md) sandbox.

## Cos&#39;è una sandbox?

Le sandbox sono partizioni virtuali all&#39;interno di una singola istanza di  Experience Platform. Ogni sandbox mantiene una propria libreria indipendente di risorse Piattaforma (inclusi schemi, set di dati, profili e così via). Tutti i contenuti e le azioni effettuate all’interno di una sandbox sono limitati a tale sandbox e non hanno effetto su altre sandbox. Per ulteriori informazioni, consultate la panoramica [delle](home.md) sandbox.

## Quali tipi di sandbox sono disponibili e quali sono le loro differenze?

 Experience Platform sono disponibili due tipi di sandbox:

* Sandbox produzione
* Sandbox non di produzione

 Experience Platform fornisce un unico sandbox **di** produzione, che non può essere eliminato o reimpostato. Per una singola istanza della piattaforma può esistere un solo sandbox di produzione.

Per contro, più sandbox **non di produzione** possono essere create dagli amministratori sandbox per una singola istanza della piattaforma. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Inoltre, le sandbox non di produzione dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. I sandbox non di produzione non possono essere convertiti in sandbox di produzione. Una licenza di Experience Platform  predefinita concede cinque sandbox (una produzione e quattro non di produzione). Potete aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox totali. Per maggiori informazioni, contattate l&#39;amministratore dell&#39;organizzazione IMS o il rappresentante commerciale  Adobe.

Per ulteriori informazioni, consultate la panoramica [delle](./home.md) sandbox.

## Posso accedere a una risorsa da più sandbox?

Le sandbox sono partizioni isolate di una singola istanza della piattaforma, con ogni sandbox che mantiene una propria libreria indipendente di risorse. Una risorsa esistente in una sandbox non è accessibile da nessun&#39;altra sandbox, indipendentemente dal tipo di sandbox (produzione o non produzione).

## Quante sandbox di produzione posso avere?

 Experience Platform supporta un solo sandbox di produzione per l&#39;organizzazione IMS, fornito out-of-the-box. La sandbox di produzione può essere rinominata ma non può essere eliminata o reimpostata. Gli utenti con autorizzazioni Amministrazione sandbox possono creare, ripristinare ed eliminare solo sandbox non di produzione.

## Quanti sandbox non di produzione posso avere?

 Experience Platform consente attualmente fino a 15 sandbox non di produzione attive in un&#39;unica organizzazione IMS.

## Ho appena creato una sandbox. Come si impostano le autorizzazioni per gli utenti che lavoreranno con questa sandbox?

Adobe Admin Console collega gli utenti alle sandbox e alle autorizzazioni tramite l&#39;uso dei profili **di** prodotto. Dopo aver creato una nuova sandbox, andate alla scheda _Autorizzazioni_ del profilo di prodotto a cui desiderate concedere l&#39;accesso, quindi fate clic su **Sandbox**. Da qui, potete aggiungere o rimuovere l&#39;accesso alla nuova sandbox allo stesso modo delle altre autorizzazioni.

Se desiderate aggiungere autorizzazioni univoche agli utenti di una particolare sandbox, potrebbe essere necessario creare un nuovo profilo di prodotto con le sandbox e le autorizzazioni appropriate applicate, e assegnare tali utenti a tale profilo.

Per ulteriori informazioni sulla gestione di sandbox e autorizzazioni nel Admin Console , consultate la guida [utente per il controllo](../access-control/ui/overview.md) degli accessi.