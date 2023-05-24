---
title: Implementare i tag JavaScript per gestire il consenso dei clienti
description: Scopri come gestire i segnali di opt-in e opt-out del cliente per diverse soluzioni Adobe in Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 93%

---

# Implementare i tag JavaScript per gestire il consenso dei clienti

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Le normative legali sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD), richiedono alle aziende di gestire il consenso per gli utenti. I clienti di Adobe possono richiedere il consenso ai visitatori prima di eseguire le soluzioni di Adobe per qualsiasi visitatore. I visitatori devono avere la possibilità di gestire il loro stato di consenso e rinuncia.

Per i clienti Adobe Experience Cloud sono necessarie diverse implementazioni di questi requisiti. Alcuni utilizzano programmi di gestione del consenso a livello enterprise, mentre altri sviluppano il proprio.

Gli sviluppatori di estensioni Adobe Experience Platform utilizzano estensioni e il generatore di regole per definire soluzioni di gestione dei consensi e delle rinunce.

Questo documento contiene informazioni su come evitare l&#39;attivazione dei tag Adobe senza l&#39;acquisizione del consenso.

## Advertising Cloud

Adobe Experience Platform non attiva automaticamente [!DNL Advertising Cloud]. [!DNL Advertising Cloud] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Traccia conversione.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.

## Analytics

Nella sezione Tracciamento collegamenti delle impostazioni di configurazione dell&#39;estensione [!DNL Analytics], accertati di *non* aver selezionato quanto segue:

* Traccia collegamenti di download
* Traccia collegamenti in uscita

Se queste impostazioni non sono selezionate, Platform non attiva automaticamente [!DNL Adobe Analytics]. [!DNL Analytics] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Invia beacon.

Puoi inoltre provare a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.

## Audience Manager

DIL è attualmente impostato per l&#39;attivazione automatica se posizionato in una pagina del cliente. Prova a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

[!DNL Adobe] consiglia di utilizzare l&#39;inoltro lato server in [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] attualmente si attiva in automatico se posizionato in una pagina del cliente.

Prova a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

## Target

Adobe Experience Platform non attiva automaticamente [!DNL Target]. [!DNL Target] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Carica di [!DNL Target].

Puoi inoltre provare a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.
