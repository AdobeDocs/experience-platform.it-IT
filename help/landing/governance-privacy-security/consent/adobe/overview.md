---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione del consenso in Adobe Experience Platform
description: Scopri come elaborare i segnali di consenso dei clienti in Adobe Experience Platform utilizzando lo standard Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# Elaborazione del consenso in Adobe Experience Platform

Adobe Experience Platform ti consente di elaborare i dati sul consenso raccolti dai clienti e di integrarli nei profili dei clienti memorizzati. Questi dati possono quindi essere utilizzati dai processi a valle per determinare se la raccolta dei dati avviene per un cliente specifico o se i loro profili vengono utilizzati per scopi specifici. Ad esempio, i dati sul consenso per un particolare profilo possono determinare se può essere incluso in un segmento di pubblico esportato o se può partecipare a canali di marketing specifici come e-mail, messaggi di testo o notifiche push.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati della Platform per acquisire i dati sul consenso dei clienti generati da una piattaforma di gestione del consenso (CMP) e integrarli nei profili dei clienti per i casi di utilizzo a valle.

>[!NOTE]
>
>Questo documento si concentra sull’elaborazione dei dati sul consenso utilizzando lo standard Adobe. Se elabori i dati sul consenso in conformità con IAB Transparency and Consent Framework (TCF) 2.0, consulta la guida su [Supporto di TCF 2.0 in Adobe Real-time Customer Data Platform](../iab/overview.md).

## Prerequisiti

Questa guida richiede una buona conoscenza dei vari servizi Experienci Platform coinvolti nel trattamento dei dati del consenso:

* [Experience Data Model (XDM)](../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
* [Servizio Adobe Experience Platform Identity](../../../../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull’esperienza del cliente, collegando le identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../../../profile/home.md): utilizza [!DNL Identity Service] funzionalità per creare in tempo reale profili cliente dettagliati dai set di dati. Real-Time Customer Profile estrae dati dal Data Lake e mantiene i profili dei clienti nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): libreria JavaScript lato client che consente di integrare vari servizi Platform nel sito web rivolto al cliente.
   * [Comandi di consenso SDK](../../../../edge/consent/supporting-consent.md): panoramica del caso d’uso dei comandi SDK relativi al consenso mostrati in questa guida.
* [Servizio di segmentazione di Adobe Experience Platform](../../../../segmentation/home.md): consente di dividere i dati del Profilo cliente in tempo reale in gruppi di individui che condividono caratteristiche simili e rispondono in modo simile alle strategie di marketing.

## Riepilogo del flusso di elaborazione del consenso {#summary}

Di seguito viene descritto come i dati di consenso vengono elaborati dopo che il sistema è stato configurato correttamente:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito web.
1. A ogni caricamento di pagina (o quando la CMP rileva una modifica nelle preferenze di consenso), uno script personalizzato sul sito mappa le preferenze correnti su un oggetto XDM standard. Questo oggetto viene quindi passato a Platform Web SDK `setConsent` comando.
1. Quando `setConsent` Si chiama, Platform Web SDK controlla se i valori del consenso sono diversi da quelli ricevuti l’ultima volta. Se i valori sono diversi (o non esiste un valore precedente), i dati strutturati sul consenso/preferenza vengono inviati a Adobe Experience Platform.
1. I dati di consenso/preferenza vengono acquisiti in una [!DNL Profile]Set di dati abilitato con schema contenente campi di consenso/preferenza.

Oltre ai comandi SDK attivati dagli hook di modifica del consenso CMP, i dati del consenso possono anche fluire in Experienci Platform tramite qualsiasi dato XDM generato dal cliente e caricato direttamente in un [!DNL Profile]Set di dati abilitato da.

### Applicazione del consenso

Nell’attuale versione del supporto per l’elaborazione del consenso in Platform, solo l’autorizzazione per la raccolta dei dati (`collect.val`) viene applicato automaticamente da Platform Web SDK. Anche se i consensi e le preferenze più granulari possono essere raccolti e memorizzati nei profili dei clienti, questi segnali aggiuntivi devono essere applicati manualmente nei processi a valle.

>[!NOTE]
>
>Per ulteriori informazioni sulla struttura dei campi di consenso XDM menzionati in precedenza, consulta la guida sulla [[!UICONTROL Consensi e preferenze] tipo di dati](../../../../xdm/data-types/consents.md).

Una volta configurato il sistema, Platform Web SDK interpreta il valore del consenso per la raccolta dati per l’utente corrente per determinare se i dati devono essere inviati alla rete Edge di Adobe Experience Platform, eliminati dal client o memorizzati finché l’autorizzazione per la raccolta dati non viene impostata su sì o no.

## Determinare come generare i dati sul consenso dei clienti all’interno della CMP {#consent-data}

Poiché ogni sistema CMP è univoco, devi determinare il modo migliore per consentire ai clienti di fornire il consenso durante l’interazione con il servizio. Un modo comune per ottenere questo risultato è utilizzare una finestra di dialogo di consenso dei cookie, simile all’esempio seguente:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Questa finestra di dialogo dovrebbe consentire al cliente di dare o rinunciare a casi d’uso specifici di marketing e personalizzazione per i propri dati. Tali consensi e preferenze devono essere conformi al modello di dati definito per il [!DNL Profile]set di dati abilitato nel passaggio successivo.

## Aggiungere campi di consenso standardizzati a [!DNL Profile]Set di dati abilitato {#dataset}

I dati sul consenso del cliente devono essere inviati a un [!DNL Profile]Set di dati abilitato con schema contenente campi di consenso. Questi campi devono essere inclusi nello stesso schema e set di dati utilizzati per acquisire informazioni sugli attributi dei singoli clienti.

Fai riferimento al tutorial su [configurazione di un set di dati per l’acquisizione dei dati sul consenso](./dataset.md) per i passaggi dettagliati su come aggiungere questi campi obbligatori a [!DNL Profile]: set di dati abilitato prima di continuare con questa guida.

## Aggiorna [!DNL Profile] criteri di unione per includere i dati sul consenso {#merge-policies}

Dopo aver creato un’ [!DNL Profile]: set di dati abilitato per l’elaborazione dei dati sul consenso, devi assicurarti che i criteri di unione siano stati configurati in modo da includere sempre i campi del consenso in ciascun profilo cliente. Ciò comporta l’impostazione della precedenza dei set di dati in modo che il set di dati di consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

>[!NOTE]
>
>Se non si dispone di set di dati in conflitto, è necessario impostare la precedenza delle marche temporali per il criterio di unione. Questo consente di garantire che l’impostazione di consenso utilizzata sia l’ultimo consenso specificato da un cliente.

Per ulteriori informazioni su come utilizzare i criteri di unione, leggere [panoramica dei criteri di unione](../../../../profile/merge-policies/overview.md). Quando configuri i criteri di unione, devi assicurarti che i profili includano tutti gli attributi di consenso richiesti forniti da [!UICONTROL Consensi e preferenze] gruppo di campi schema, come descritto nella guida su [preparazione set di dati](./dataset.md).

## Portare i dati del consenso in Platform

Una volta che disponi dei set di dati e dei criteri di unione per rappresentare i campi di consenso richiesti nei profili dei clienti, il passaggio successivo consiste nell’inserire i dati di consenso stessi in Platform.

Principalmente, devi utilizzare Adobe Experience Platform Web SDK per inviare i dati sul consenso a Platform ogni volta che la CMP rileva eventi di modifica del consenso. Se raccogli i dati sul consenso su una piattaforma mobile, devi utilizzare l’SDK di Adobe Experience Platform Mobile. Puoi anche scegliere di acquisire direttamente i dati di consenso raccolti mappandoli sullo schema XDM del set di dati di consenso e inviandoli a Platform tramite l’acquisizione batch.

I dettagli di ciascuno di questi metodi sono forniti nelle sottosezioni seguenti.

### Configurare l’SDK per web di Experienci Platform per elaborare i dati sul consenso {#web-sdk}

Dopo aver configurato la CMP per l’ascolto degli eventi di modifica del consenso sul sito web, puoi integrare Experienci Platform Web SDK per ricevere le impostazioni di consenso aggiornate e inviarle a Platform a ogni caricamento di pagina e ogni volta che si verificano eventi di modifica del consenso. Consulta la guida su [configurazione di Web SDK per elaborare i dati sul consenso dei clienti](../sdk.md) per ulteriori informazioni.

### Configurare l’SDK di Experienci Platform Mobile per elaborare i dati sul consenso {#mobile-sdk}

Se nell’app mobile sono richieste le preferenze di consenso del cliente, puoi integrare l’SDK di Experienci Platform Mobile per recuperare e aggiornare le impostazioni del consenso, inviandole a Platform ogni volta che viene chiamata l’API di consenso.

Consulta la documentazione dell’SDK di Mobile per [configurazione dell’estensione per dispositivi mobili di consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) e [utilizzo dell’API di consenso](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Per ulteriori dettagli su come gestire i problemi di privacy utilizzando l’SDK di Mobile, consulta la sezione [Privacy e RGPD](https://developer.adobe.com/client-sdks/documentation/resources/privacy-and-gdpr/).

### Acquisire direttamente i dati di consenso conformi a XDM {#batch}

Puoi acquisire dati di consenso conformi a XDM da un file CSV utilizzando l’acquisizione batch. Questo può essere utile se disponi di un backlog di dati sul consenso raccolti in precedenza che non è ancora stato integrato nei profili dei clienti.

Segui l’esercitazione su [mappatura di un file CSV su XDM](../../../../ingestion/tutorials/map-csv/overview.md) per scoprire come convertire i campi dati in XDM e acquisirli in Platform. Quando si seleziona [!UICONTROL Destinazione] per la mappatura, accertati di selezionare **[!UICONTROL Usa set di dati esistente]** e scegli la [!DNL Profile]Set di dati di consenso creato in precedenza abilitato.

## Testare l’implementazione {#test-implementation}

Dopo aver acquisito i dati sul consenso dei clienti nel tuo [!DNL Profile]: set di dati abilitato, puoi controllare i profili aggiornati per verificare se contengono attributi di consenso.

>[!IMPORTANT]
>
>Per visualizzare gli attributi di un profilo esistente nell’interfaccia utente, è necessario conoscere almeno un valore di identità (e il relativo spazio dei nomi corrispondente) associato a tale profilo.
>
>Se non hai accesso a queste informazioni, puoi scegliere di acquisire i tuoi dati di consenso di test e associarli a un valore di identità/spazio dei nomi che è noto a te.

Consulta la sezione su [esplorazione dei profili per identità](../../../../profile/ui/user-guide.md#browse) nel [!DNL Profile] Guida all’interfaccia utente per i passaggi specifici su come cercare i dettagli di un profilo.

Per impostazione predefinita, i nuovi attributi di consenso non vengono visualizzati nel dashboard di un profilo. Pertanto, devi passare al **[!UICONTROL Attributi]** nella pagina dei dettagli di un profilo per confermare che sono stati acquisiti come previsto. Consulta la guida sulla [dashboard dei profili](../../../../profile/ui/profile-dashboard.md) per scoprire come personalizzare il dashboard in base alle proprie esigenze.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Passaggi successivi

Questa guida illustra come configurare le operazioni di Platform per elaborare i dati sul consenso dei clienti utilizzando lo standard Adobe e come rappresentare tali attributi nei profili cliente. Ora puoi integrare le preferenze di consenso dei clienti come fattore determinante nella qualificazione dei segmenti e in altri casi d’uso a valle.

Per ulteriori informazioni sulle funzionalità di Experienci Platform relative alla privacy, consulta la panoramica su [governance, privacy e sicurezza in Platform](../../overview.md).
