---
keywords: Experience Platform;home;argomenti comuni;risoluzione dei problemi sandbox
solution: Experience Platform
title: Guida alla risoluzione dei problemi delle sandbox
topic-legacy: troubleshooting guide
description: Questo documento fornisce le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi delle sandbox

Questo documento fornisce le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi di Platform, consulta la [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Le sandbox suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](home.md) .

## Cos&#39;è una sandbox?

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni sandbox mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati, profili e così via). Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non hanno alcun effetto su altre sandbox. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](home.md) .

## Quali tipi di sandbox sono disponibili e quali sono le loro differenze?

Nell’Experience Platform sono disponibili due tipi di sandbox:

* Sandbox di produzione
* Sandbox non di produzione

Experience Platform fornisce una singola sandbox di produzione, che non può essere eliminata o reimpostata. Per una singola istanza di Platform può esistere una sola sandbox di produzione.

Al contrario, più sandbox non di produzione possono essere create dagli amministratori di sandbox per una singola istanza di Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Inoltre, le sandbox non di produzione hanno una funzione di reimpostazione che rimuove tutte le risorse create dal cliente dalla sandbox. Le sandbox non di produzione non possono essere convertite in sandbox di produzione. Una licenza di Experience Platform predefinita concede cinque sandbox (una produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox totali. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione IMS o il rappresentante commerciale di Adobe.

Per ulteriori informazioni, consulta la [panoramica sulle sandbox](./home.md) .

## Posso accedere a una risorsa da più di una sandbox?

Le sandbox sono partizioni isolate di una singola istanza di Platform, con ogni sandbox che mantiene la propria libreria indipendente di risorse. Una risorsa esistente in una sandbox non è accessibile da nessun’altra sandbox, indipendentemente dal tipo di sandbox (produzione o non produzione).

## Quante sandbox di produzione posso avere?

Experience Platform supporta solo una sandbox di produzione per l’organizzazione IMS, fornita come standard. La sandbox di produzione può essere rinominata ma non può essere eliminata o reimpostata. Gli utenti con autorizzazioni di amministrazione sandbox possono solo creare, reimpostare ed eliminare sandbox non di produzione.

## Quante sandbox non di produzione posso avere?

Experience Platform consente attualmente l’attivazione di fino a 15 sandbox non di produzione all’interno di un’unica organizzazione IMS.

## Ho appena creato una sandbox. Come si impostano le autorizzazioni per gli utenti che lavoreranno con questa sandbox?

Adobe Admin Console collega gli utenti alle sandbox e alle autorizzazioni tramite l’uso dei profili di prodotto. Dopo aver creato una nuova sandbox, passa alla scheda **Autorizzazioni** del profilo di prodotto a cui desideri concedere l’accesso, quindi fai clic su **Sandbox**. Da qui, puoi aggiungere o rimuovere l’accesso alla nuova sandbox nello stesso modo di altre autorizzazioni.

Se desideri aggiungere autorizzazioni univoche agli utenti di una particolare sandbox, potrebbe essere necessario creare un nuovo profilo di prodotto con le sandbox e le autorizzazioni appropriate applicate e assegnare tali utenti a tale profilo.

Per ulteriori informazioni sulla gestione delle sandbox e delle autorizzazioni nell’Admin Console, consulta la [guida utente per il controllo degli accessi](../access-control/ui/overview.md) .
