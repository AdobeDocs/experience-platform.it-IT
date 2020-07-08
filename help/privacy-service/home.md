---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Adobe Experience Platform Privacy Service '
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Panoramica del Adobe Experience Platform Privacy Service 

Per offrire esperienze cliente migliori, devi raccogliere e archiviare i dati personali dei clienti. Quando si utilizzano questi dati, è importante comprendere e rispettare la privacy dei clienti. Le nuove normative legali e organizzative danno agli utenti il diritto di accedere o cancellare i propri dati personali dall&#39;archivio dei dati su richiesta.

 Adobe Experience Platform Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente per aiutarti a gestire queste richieste di dati dai clienti. Con Privacy Service, puoi inviare richieste di accesso ed eliminazione di dati di clienti privati o personali dalle applicazioni Adobe Experience Cloud, per facilitare la conformità automatica alle normative sulla privacy legali e organizzative.

## Perché Privacy Service?

Privacy Service è stata sviluppata in risposta a un cambiamento fondamentale nel modo in cui le aziende sono tenute a gestire i dati personali dei loro clienti. Lo scopo principale di Privacy Service è automatizzare la conformità alle normative sulla privacy dei dati che, in caso di violazione, possono comportare multe elevate e interrompere le operazioni relative ai dati per la tua attività.

### Privacy Service e GDPR

Il [](https://eugdpr.org/)Regolamento generale sulla protezione dei dati (RGPD) ha introdotto diversi nuovi diritti riguardanti la privacy dei dati per i membri dell’Unione europea, tra cui il **diritto di accesso** e il **diritto all’oblio**. Ciò significa che qualsiasi cittadino dell’UE i cui dati personali siano stati raccolti dalla tua azienda può richiedere l’accesso ai dati o la loro cancellazione in qualsiasi momento. Il mancato rispetto di queste richieste entro 30 giorni può comportare multe per più milioni di dollari per la tua organizzazione.

Privacy Service supporta le richieste di accesso ed eliminazione per il GDPR e le tiene traccia separatamente rispetto alle richieste previste dal regolamento CCPA. Per ulteriori informazioni, consulta le Domande frequenti [e i documenti](gdpr/faq.md) terminologici [](gdpr/terminology.md) del GDPR.

### Privacy Service e CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. L&#39;CCPA fornisce nuovi diritti sulla privacy dei dati ai residenti della California, compreso il diritto di accedere ai loro dati personali ed eliminarli, di sapere se i loro dati personali sono venduti o divulgati (e a chi), e il diritto di non far vendere i loro dati a terzi.

Privacy Service supporta le richieste di accesso ed eliminazione per la normativa CCPA e le tiene traccia separatamente dalle richieste GDPR. Privacy Service supporta anche l&#39;invio di richieste di rinuncia alla vendita per  applicazioni Experience Cloud che le supportano. Per ulteriori informazioni, consulta [le Domande frequenti](ccpa/faq.md) sull’applicazione CCPA.

## Come utilizzare Privacy Service per gestire le richieste di lavoro sulla privacy

Privacy Service fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire le richieste dei clienti di accedere/eliminare i loro dati privati o di rinunciare alla vendita (noti anche come processi **di** privacy). Il servizio fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di visualizzare lo stato e i risultati dei processi di privacy che coinvolgono  applicazioni Experience Cloud.

>[!NOTE]
>
>Le richieste di rifiuto al momento sono supportate solo dall&#39;API Privacy Service.

### Utilizzo dell&#39;API

L&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service consente di creare e gestire i processi relativi alla privacy mediante chiamate RESTful API, consentendo di impostare in modo programmatico la conformità alla normativa sulla privacy per le applicazioni Experience Cloud . Per i passaggi dettagliati su come utilizzare l&#39;API, consultate la guida [per gli sviluppatori di](api/getting-started.md)Privacy Service API.

### Utilizzo dell’interfaccia

L’interfaccia utente di Privacy Service consente di creare e monitorare i processi relativi alla privacy mediante un’interfaccia grafica. L’interfaccia utente include un widget per report **di** stato che fornisce una rappresentazione visiva dello stato di tutte le richieste attive e consente di creare nuove richieste utilizzando il **Generatore** di richieste incorporato o caricando file JSON. Per ulteriori informazioni sull’utilizzo dell’interfaccia utente, consultate la guida [utente di](ui/overview.md)Privacy Service.