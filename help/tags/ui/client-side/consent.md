---
title: Implementare i tag JavaScript per gestire il consenso dei clienti
description: Scopri come gestire i segnali di opt-in e opt-out del cliente per diverse soluzioni Adobe in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 87%

---

# Implementare i tag JavaScript per gestire il consenso dei clienti

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

La combinazione del [Regolamento generale sulla protezione dei dati (GDPR)](https://gdpr-info.eu/art-7-gdpr/) e [la direttiva ePrivacy](https://medium.com/mydata/consent-lost-gdpr-and-found-eprivacy-e85cf881ffb) dell&#39;Unione Europea richiede alle aziende di gestire il consenso per gli utenti. I clienti di Adobe possono richiedere il consenso ai visitatori prima che le soluzioni di Adobe vengano eseguite per un determinato visitatore. I visitatori devono avere la possibilità di gestire il loro stato di consenso e rinuncia.

I clienti Adobe Experience Cloud richiedono diverse implementazioni di questi requisiti. Alcuni utilizzano programmi di gestione del consenso a livello enterprise, mentre altri sviluppano il proprio.

Gli sviluppatori di estensioni Adobe Experience Platform utilizzano le estensioni e il generatore di regole per definire soluzioni di consenso e rinuncia.

Questo documento contiene informazioni su come evitare l&#39;attivazione dei tag Adobe senza l&#39;acquisizione del consenso.

## Advertising Cloud

Adobe Experience Platform non attiva automaticamente [!DNL Advertising Cloud]. [!DNL Advertising Cloud] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Traccia conversione.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.

## Analytics

Nella sezione Tracciamento collegamenti delle impostazioni di configurazione dell&#39;estensione [!DNL Analytics], accertati di *non* aver selezionato quanto segue:

* Traccia collegamenti di download
* Traccia collegamenti in uscita

Se queste impostazioni non sono selezionate, Platform non attiva automaticamente [!DNL Adobe Analytics] . [!DNL Analytics] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Invia beacon.

Puoi inoltre provare a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=it) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.

## Audience Manager

DIL è attualmente impostato per l&#39;attivazione automatica se posizionato in una pagina del cliente. Prova a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

[!DNL Adobe] consiglia di utilizzare l&#39;inoltro lato server in [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] attualmente si attiva in automatico se posizionato in una pagina del cliente.

Prova a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

## Target

Adobe Experience Platform non attiva automaticamente [!DNL Target]. [!DNL Target] si attiva solo se espressamente indicato in un&#39;azione di una regola. Utilizza le condizioni della regola per determinare quando e cosa attivare. Ad esempio, per utilizzare i cookie di determinazione dello stato del consenso, imposta un elemento di dati per leggere tale cookie e utilizzalo come condizione nella regola per determinare quando attivare l&#39;azione Carica di [!DNL Target].

Puoi inoltre provare a utilizzare [l’oggetto Adobe opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) per controllare l&#39;attivazione di questo tag insieme alla piattaforma per la gestione del consenso.

Le integrazioni con i programmi di gestione del consenso (ad esempio OneTrust) possono impostare e tenere traccia dei cookie di consenso per i clienti, che possono quindi essere utilizzati nel generatore di regole.
