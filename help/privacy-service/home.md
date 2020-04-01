---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servizio Privacy di Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Panoramica di Adobe Experience Platform Privacy Service

Per offrire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta.

Il servizio Adobe Experience Platform Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai tuoi clienti. Il servizio Privacy consente di inviare richieste per l&#39;accesso e l&#39;eliminazione di dati privati o personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatizzata alle normative sulla privacy legali e organizzative.

## Perché il servizio sulla privacy?

Il servizio sulla privacy è stato sviluppato in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. L&#39;obiettivo principale del Servizio per la privacy è automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, possono comportare gravi multe e interrompere le operazioni relative ai dati per la tua attività.

### Privacy Service e GDPR

Il Regolamento [](https://eugdpr.org/) generale sulla protezione dei dati (GDPR) ha introdotto diversi nuovi diritti sulla privacy dei dati per i membri dell&#39;Unione europea, tra cui il **Diritto di accesso** e il **Diritto di essere Dimenticato**. Ciò significa che qualsiasi cittadino dell&#39;UE i cui dati personali siano stati raccolti dalla tua azienda può richiedere l&#39;accesso o l&#39;eliminazione dei dati in qualsiasi momento. Il mancato rispetto di queste richieste entro 30 giorni può comportare multe per più milioni di dollari per la tua organizzazione.

Il servizio per la privacy supporta le richieste di accesso ed eliminazione del GDPR e le tiene traccia separatamente rispetto alle richieste previste dal regolamento CCPA. Per ulteriori informazioni, consulta le Domande frequenti [e i documenti](gdpr/faq.md) terminologici [](gdpr/terminology.md) del GDPR.

### Privacy Service e CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. L&#39;CCPA fornisce nuovi diritti sulla privacy dei dati ai residenti della California, compreso il diritto di accedere ai loro dati personali ed eliminarli, di sapere se i loro dati personali sono venduti o divulgati (e a chi), e il diritto di non far vendere i loro dati a terzi.

Il servizio Privacy supporta le richieste di accesso ed eliminazione per il regolamento CCPA e le tiene traccia separatamente dalle richieste GDPR. Il servizio per la privacy supporta anche l&#39;invio di richieste di rinuncia alla vendita per le applicazioni Experience Cloud che le supportano. Per ulteriori informazioni, consulta [le Domande frequenti](ccpa/faq.md) sull’applicazione CCPA.

## Come utilizzare il servizio sulla privacy per gestire le richieste di lavoro sulla privacy

Il servizio Privacy fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire le richieste dei clienti di accedere/cancellare i loro dati privati o di rinunciare alla vendita (o di **effettuare dei processi** sulla privacy). Il servizio fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di visualizzare lo stato e i risultati dei processi relativi alla privacy che coinvolgono le applicazioni Experience Cloud.

>[!NOTE] Al momento le richieste di rifiuto sono supportate solo dall&#39;API del servizio sulla privacy.

### Utilizzo dell&#39;API

L&#39;API [del servizio](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy consente di creare e gestire i processi relativi alla privacy mediante chiamate RESTful API, consentendo di impostare in modo programmatico la conformità alla normativa sulla privacy per le applicazioni Experience Cloud. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, consultate la guida per gli sviluppatori dell&#39;API [Privacy Service](api/getting-started.md).

### Utilizzo dell’interfaccia

L’interfaccia utente del servizio Privacy consente di creare e monitorare i processi relativi alla privacy mediante un’interfaccia grafica. L’interfaccia utente include un widget per report **di** stato che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **Generatore** di richieste incorporato o caricando file JSON. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente, consulta la guida [utente del servizio](ui/overview.md)per la privacy.