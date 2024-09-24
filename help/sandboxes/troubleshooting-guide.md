---
keywords: Experience Platform;home;argomenti popolari;risoluzione dei problemi sandbox
solution: Experience Platform
title: Guida alla risoluzione dei problemi relativi alle sandbox
description: Questo documento fornisce le risposte alle domande più frequenti sulle sandbox in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 8%

---

# Guida alla risoluzione dei problemi relativi alle sandbox

Questo documento fornisce le risposte alle domande più frequenti sulle sandbox in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, consulta la [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Le sandbox suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale. Per ulteriori informazioni, consulta la [panoramica delle sandbox](home.md).

## Che cos’è un sandbox?

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni sandbox mantiene la propria libreria indipendente di risorse di Platform (inclusi schemi, set di dati, profili e così via). Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non influiscono su altre sandbox. Per ulteriori informazioni, consulta la [panoramica delle sandbox](home.md).

## Quali tipi di sandbox sono disponibili e quali sono le loro differenze? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo di sandbox"
>abstract="Il tipo di sandbox indica se si tratta di una sandbox di produzione o di sviluppo. Le sandbox di produzione includono dati in tempo reale; quelle di sviluppo vengono utilizzate a scopo di test e sviluppo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=it#create" text="Creare una sandbox nell’interfaccia utente"

In Experience Platform sono disponibili due tipi di sandbox:

* **Sandbox di produzione**: una sandbox di produzione deve essere utilizzata con i profili nell&#39;ambiente di produzione. Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati, mantenendo al contempo l’isolamento operativo. Questa funzione consente di dedicare specifiche sandbox di produzione a linee di business, marchi, progetti o aree geografiche distinte. Le sandbox di produzione supportano un volume di profili di produzione fino all&#39;impegno [!DNL Profile] concesso in licenza (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai diritto a utilizzare l’intero volume totale di dati concesso in licenza (misurato cumulativamente in tutte le sandbox di produzione autorizzate).

* **Sandbox di sviluppo**: una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% dell&#39;impegno [!DNL Profile] concesso in licenza (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto a:
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 chiamate API [!DNL Profile], per [!DNL Profile], all&#39;anno (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate.

Per ulteriori informazioni, consulta la [panoramica delle sandbox](./home.md).

## È possibile accedere a una risorsa da più sandbox?

Le sandbox sono partizioni isolate di una singola istanza Platform e ogni sandbox mantiene la propria libreria indipendente di risorse. Non è possibile accedere a una risorsa presente in una sandbox da nessun’altra sandbox, indipendentemente dal tipo di sandbox (di produzione o non di produzione).

## Qual è la sandbox di produzione predefinita?

La sandbox di produzione predefinita è la prima sandbox di produzione creata al primo provisioning di un’organizzazione. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Platform, nonché di accettare richieste che non includono valori per il nome di una sandbox o l’ID di una sandbox. La sandbox di produzione predefinita può essere reimpostata ma non eliminata.

## Quante sandbox di produzione posso avere?

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo, ciascuna delle quali mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati e profili).

Una licenza di Experience Platform predefinita ti concede un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. Puoi concedere in licenza pacchetti aggiuntivi di 10 sandbox per un massimo di 75 sandbox in totale.

Le sandbox di produzione possono essere reimpostate o eliminate, ad eccezione di quelle utilizzate anche da Adobe Analytics per la funzione [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it), oppure se il grafo delle identità ospitato al suo interno è utilizzato anche da Adobe Audience Manager per la funzione [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it).

Puoi aggiornare il titolo di una sandbox di produzione. Tuttavia, non è possibile rinominare una sandbox di produzione.

>[!NOTE]
>
>Il nome della sandbox viene utilizzato a scopo di ricerca nelle chiamate API, mentre il titolo della sandbox viene utilizzato come nome visualizzato.

## Quante sandbox di sviluppo posso avere?

Experience Platform attualmente consente di attivare un massimo di 75 sandbox totali (produzione e sviluppo) all’interno di una singola organizzazione.

Le sandbox di sviluppo supportano sia le funzionalità di ripristino che quelle di eliminazione.

## Ho appena creato una sandbox. Come si impostano le autorizzazioni per gli utenti che lavoreranno con questa sandbox?

Adobe Admin Console collega gli utenti alle sandbox e alle autorizzazioni tramite l’utilizzo dei profili di prodotto. Dopo aver creato una nuova sandbox, passa alla scheda **Autorizzazioni** del profilo di prodotto a cui desideri concedere l&#39;accesso, quindi fai clic su **Sandbox**. Da qui, puoi aggiungere o rimuovere l’accesso alla nuova sandbox nello stesso modo delle altre autorizzazioni.

Se desideri aggiungere autorizzazioni univoche agli utenti di una particolare sandbox, potrebbe essere necessario creare un nuovo profilo di prodotto applicando le sandbox e le autorizzazioni appropriate e assegnare tali utenti a quel profilo.

Per ulteriori informazioni sulla gestione delle sandbox e delle autorizzazioni, consulta la [guida utente per il controllo degli accessi](../access-control/ui/overview.md) nell&#39;Admin Console.
