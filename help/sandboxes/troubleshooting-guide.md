---
keywords: Experience Platform;home;argomenti comuni;risoluzione dei problemi sandbox
solution: Experience Platform
title: Guida alla risoluzione dei problemi delle sandbox
description: Questo documento fornisce le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Guida alla risoluzione dei problemi delle sandbox

Questo documento fornisce le risposte alle domande frequenti sulle sandbox in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi Platform, consulta la sezione [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

Le sandbox suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale. Consulta la sezione [panoramica sulle sandbox](home.md) per ulteriori informazioni.

## Cos&#39;è una sandbox?

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni sandbox mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati, profili e così via). Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non hanno alcun effetto su altre sandbox. Consulta la sezione [panoramica sulle sandbox](home.md) per ulteriori informazioni.

## Quali tipi di sandbox sono disponibili e quali sono le loro differenze? {#sandbox-types}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtypes"
>title="Tipo di sandbox"
>abstract="Il tipo di sandbox indica se si tratta di una sandbox di produzione o di sviluppo. Le sandbox di produzione includono dati live e sandbox di sviluppo vengono utilizzate per il test e lo sviluppo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html#create" text="Creare una sandbox nell’interfaccia utente"

Nell’Experience Platform sono disponibili due tipi di sandbox:

* **Sandbox di produzione**: Una sandbox di produzione deve essere utilizzata con i profili nell’ambiente di produzione. Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati mantenendo al tempo stesso l’isolamento operativo. Questa funzione consente di dedicare sandbox di produzione specifiche a linee di business, marchi, progetti o aree geografiche diverse. Le sandbox di produzione supportano un volume di profili di produzione fino al vostro sotto licenza [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai il diritto di utilizzare il profilo medio concesso in licenza per ogni autorizzato [!DNL Profile] (misurato cumulativamente in tutte le sandbox di produzione autorizzate).
* **Sandbox di sviluppo**: Una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% della licenza [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto fino a:
   * una ricchezza media di profilo non di produzione di 75 kilobyte per profilo non di produzione autorizzato (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate);
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 [!DNL Profile] Chiamate API, per [!DNL Profile], per anno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate.

Consulta la sezione [panoramica sulle sandbox](./home.md) per ulteriori informazioni.

## Posso accedere a una risorsa da più di una sandbox?

Le sandbox sono partizioni isolate di una singola istanza di Platform, con ogni sandbox che mantiene la propria libreria indipendente di risorse. Una risorsa esistente in una sandbox non è accessibile da nessun’altra sandbox, indipendentemente dal tipo di sandbox (produzione o non produzione).

## Qual è la sandbox di produzione predefinita?

La sandbox di produzione predefinita è la prima sandbox di produzione che viene creata al momento del primo provisioning di un&#39;organizzazione. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Platform, nonché di accettare richieste che non includono valori per un nome sandbox o un ID sandbox. La sandbox di produzione predefinita può essere reimpostata ma non eliminata.

## Quante sandbox di produzione posso avere?

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo, con ogni sandbox che mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati e profili).

Una licenza di Experience Platform predefinita ti concede un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. È possibile concedere in licenza pacchetti aggiuntivi di 10 sandbox fino a un massimo di 75 sandbox in totale.

Le sandbox di produzione possono essere reimpostate o eliminate, ad eccezione delle sandbox di produzione che vengono utilizzate anche da Adobe Analytics per la [Analisi multidispositivo (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) o se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Audience Manager per [Destinazioni basate su persone (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it) funzionalità.

Puoi aggiornare il titolo di una sandbox di produzione. Tuttavia, non è possibile rinominare una sandbox di produzione.

>[!NOTE]
>
>Il nome della sandbox viene utilizzato a scopo di ricerca nelle chiamate API, mentre il titolo della sandbox viene utilizzato come nome visualizzato.

## Quante sandbox di sviluppo posso avere?

L’Experience Platform consente attualmente l’attività di un massimo di 75 sandbox totali (produzione e sviluppo) all’interno di un’unica organizzazione.

Le sandbox di sviluppo supportano sia le funzionalità di ripristino che quelle di eliminazione.

## Ho appena creato una sandbox. Come si impostano le autorizzazioni per gli utenti che lavoreranno con questa sandbox?

Adobe Admin Console collega gli utenti alle sandbox e alle autorizzazioni tramite l’uso dei profili di prodotto. Dopo aver creato una nuova sandbox, passa alla **Autorizzazioni** scheda del profilo di prodotto a cui desideri concedere l’accesso, quindi fai clic su **Sandbox**. Da qui, puoi aggiungere o rimuovere l’accesso alla nuova sandbox nello stesso modo di altre autorizzazioni.

Se desideri aggiungere autorizzazioni univoche agli utenti di una particolare sandbox, potrebbe essere necessario creare un nuovo profilo di prodotto con le sandbox e le autorizzazioni appropriate applicate e assegnare tali utenti a tale profilo.

Consulta la sezione [guida utente per il controllo degli accessi](../access-control/ui/overview.md) per ulteriori informazioni sulla gestione di sandbox e autorizzazioni nell’Admin Console.
