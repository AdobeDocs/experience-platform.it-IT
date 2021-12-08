---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione del consenso in Adobe Experience Platform
topic-legacy: getting started
description: Scopri come elaborare i segnali di consenso dei clienti in Adobe Experience Platform utilizzando lo standard Adobe 2.0.
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f9ccce8943e2aaf65cd3e0ffe2b974a668bba9b7
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 0%

---

# Elaborazione del consenso in Adobe Experience Platform

Adobe Experience Platform ti consente di elaborare i dati sul consenso raccolti dai clienti e di integrarli nei profili cliente memorizzati. Questi dati possono quindi essere utilizzati dai processi a valle per determinare se la raccolta dei dati avviene per un cliente specifico o se i profili sono utilizzati per scopi specifici. Ad esempio, i dati di consenso per un particolare profilo possono determinare se può essere incluso in un segmento di pubblico esportato o se può partecipare a canali di marketing specifici come e-mail, messaggi di testo o notifiche push.

Questo documento fornisce una panoramica su come configurare le operazioni sui dati di Platform per acquisire i dati di consenso dei clienti generati da una piattaforma di gestione dei consensi (CMP) e integrarli nei profili dei clienti per i casi di utilizzo a valle.

>[!NOTE]
>
>Questo documento si concentra sull’elaborazione dei dati di consenso tramite lo standard Adobe. Se elabora i dati di consenso in conformità con IAB Transparency and Consent Framework (TCF) 2.0, consulta la guida su [Supporto TCF 2.0 in Real-time Customer Data Platform](../iab/overview.md).

## Prerequisiti

Questa guida richiede una comprensione approfondita dei vari servizi di Experience Platform coinvolti nell’elaborazione dei dati di consenso:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Servizio Adobe Experience Platform Identity](../../../../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [Profilo cliente in tempo reale](../../../../profile/home.md): Usi [!DNL Identity Service] funzionalità per creare profili cliente dettagliati dai set di dati in tempo reale. Il profilo cliente in tempo reale richiama i dati dal Data Lake e persiste nei profili cliente nel proprio archivio dati separato.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Libreria JavaScript lato client che consente di integrare vari servizi Platform nel sito web rivolto ai clienti.
   * [Comandi di consenso SDK](../../../../edge/consent/supporting-consent.md): Panoramica del caso d’uso dei comandi SDK relativi al consenso visualizzati in questa guida.
* [Servizio di segmentazione di Adobe Experience Platform](../../../../segmentation/home.md): Consente di dividere i dati Profilo cliente in tempo reale in gruppi di persone che condividono caratteristiche simili e risponderanno in modo simile alle strategie di marketing.

## Riepilogo del flusso di elaborazione del consenso {#summary}

Di seguito viene descritto come vengono elaborati i dati di consenso dopo che il sistema è stato configurato correttamente:

1. Un cliente fornisce le proprie preferenze di consenso per la raccolta dei dati tramite una finestra di dialogo sul sito web.
1. In ogni caricamento di pagina (o quando CMP rileva una modifica nelle preferenze di consenso), uno script personalizzato sul sito mappa le preferenze correnti a un oggetto XDM standard. Questo oggetto viene quindi passato all’SDK per web di Platform `setConsent` comando.
1. Quando `setConsent` viene chiamato , l’SDK per web di Platform controlla se i valori di consenso sono diversi da quelli ricevuti per l’ultima volta. Se i valori sono diversi (o non esiste un valore precedente), i dati strutturati di consenso/preferenza vengono inviati a Adobe Experience Platform.
1. I dati di consenso o preferenza vengono acquisiti in un [!DNL Profile]Set di dati abilitato il cui schema contiene campi di consenso/preferenza.

Oltre ai comandi SDK attivati dagli hook di CMP per la modifica del consenso, i dati di consenso possono fluire in Experience Platform attraverso qualsiasi dato XDM generato dal cliente e caricato direttamente in un [!DNL Profile]Set di dati abilitato.

### Applicazione del consenso

Nella versione corrente del supporto per l’elaborazione del consenso in Platform, solo l’autorizzazione per la raccolta dati (`collect.val`) viene applicata automaticamente dall’SDK per web di Platform. Mentre i consensi e le preferenze più granulari possono essere raccolti e mantenuti nei profili dei clienti, questi segnali aggiuntivi devono essere applicati manualmente nei tuoi processi a valle.

>[!NOTE]
>
>Per ulteriori informazioni sulla struttura dei campi di consenso XDM di cui sopra, consulta la guida sulla [[!UICONTROL Consensi e preferenze] tipo di dati](../../../../xdm/data-types/consents.md).

Una volta configurato il sistema, Platform Web SDK interpreta il valore del consenso per la raccolta dati per l’utente corrente per determinare se i dati devono essere inviati a Adobe Experience Platform Edge Network, rilasciati dal client o mantenuti fino a quando l’autorizzazione per la raccolta dati non viene impostata su sì o no.

## Determinare come generare i dati di consenso dei clienti all’interno di CMP {#consent-data}

Poiché ogni sistema CMP è univoco, devi determinare il modo migliore per consentire ai tuoi clienti di fornire il consenso mentre interagiscono con il tuo servizio. Un modo comune per ottenere questo risultato consiste nell’utilizzare una finestra di dialogo di consenso dei cookie, simile all’esempio seguente:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

Questa finestra di dialogo deve consentire al cliente di rinunciare o di accedere a casi d’uso di marketing e personalizzazione specifici per i propri dati. Questi consensi e preferenze devono essere conformi al modello dati definito per la [!DNL Profile]Set di dati abilitato nel passaggio successivo.

## Aggiungi campi di consenso standardizzati a un [!DNL Profile]set di dati abilitati {#dataset}

I dati di consenso del cliente devono essere inviati a un [!DNL Profile]Set di dati abilitato il cui schema contiene campi di consenso. Questi campi devono essere inclusi nello stesso schema e set di dati utilizzato per acquisire informazioni sugli attributi relativi ai singoli clienti.

Fai riferimento all’esercitazione su [configurazione di un set di dati per l’acquisizione dei dati di consenso](./dataset.md) per i passaggi dettagliati su come aggiungere questi campi obbligatori a un [!DNL Profile]Set di dati abilitato prima di continuare con questa guida.

## Aggiorna [!DNL Profile] unione dei criteri per includere i dati di consenso {#merge-policies}

Una volta creata una [!DNL Profile]Set di dati abilitato per l’elaborazione dei dati di consenso, è necessario assicurarsi che i criteri di unione siano stati configurati in modo da includere sempre i campi di consenso in ciascun profilo cliente. Ciò comporta l’impostazione della precedenza del set di dati in modo che il set di dati di consenso abbia priorità rispetto ad altri set di dati potenzialmente in conflitto.

>[!NOTE]
>
>Se non si dispone di set di dati in conflitto, è invece necessario impostare la precedenza delle marche temporali per il criterio di unione. In questo modo è possibile garantire che l’impostazione di consenso utilizzata sia l’impostazione più recente del consenso specificato da un cliente.

Per ulteriori informazioni su come utilizzare i criteri di unione, iniziare leggendo il [panoramica dei criteri di unione](../../../../profile/merge-policies/overview.md). Quando si impostano i criteri di unione, è necessario assicurarsi che i profili includano tutti gli attributi di consenso richiesti dalla [!UICONTROL Consensi e preferenze] gruppo di campi schema, come descritto nella guida in [preparazione dei set di dati](./dataset.md).

## Inserire i dati di consenso in Platform

Una volta che i set di dati e i criteri di unione rappresentano i campi di consenso richiesti nei profili dei clienti, il passaggio successivo consiste nell’inserire i dati di consenso in Platform.

In genere, devi utilizzare Adobe Experience Platform Web SDK per inviare dati di consenso a Platform ogni volta che la CMP rileva eventi di modifica del consenso. Se raccogli i dati di consenso su una piattaforma mobile, utilizza l’SDK di Adobe Experience Platform Mobile. Puoi anche scegliere di acquisire i dati di consenso raccolti direttamente mappandoli allo schema XDM del set di dati di consenso e inviandoli a Platform tramite l’acquisizione batch.

I dettagli relativi a ciascuno di questi metodi sono forniti nelle sottosezioni seguenti.

### Configurare Experience Platform Web SDK per elaborare i dati di consenso {#web-sdk}

Dopo aver configurato la CMP per ascoltare gli eventi relativi alla modifica del consenso sul sito web, è possibile integrare l’SDK per web di Experience Platform per ricevere le impostazioni di consenso aggiornate e inviarle a Platform a ogni caricamento di pagina e ogni volta che si verificano eventi relativi alla modifica del consenso. Consulta la guida su [configurazione dell’SDK per web per l’elaborazione dei dati sul consenso dei clienti](../sdk.md) per ulteriori informazioni.

### Configurare l’SDK di Experience Platform Mobile per elaborare i dati di consenso {#mobile-sdk}

Se nell’app mobile sono richieste le preferenze di consenso dei clienti, puoi integrare l’SDK di Experience Platform Mobile per recuperare e aggiornare le impostazioni di consenso, inviandole a Platform ogni chiamata dell’API di consenso.

Consulta la documentazione dell’SDK mobile per [configurazione dell’estensione Consent mobile](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network) e [utilizzo dell’API di consenso](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network/api-reference). Per ulteriori dettagli su come gestire i problemi di privacy utilizzando l&#39;SDK di Mobile, consulta la sezione . [Privacy e RGPD](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr).

### Inserire direttamente i dati di consenso conformi a XDM {#batch}

È possibile acquisire dati di consenso conformi a XDM da un file CSV utilizzando l’acquisizione batch. Questa funzione può essere utile se disponi di un backlog dei dati di consenso raccolti in precedenza che devono ancora essere integrati nei profili dei clienti.

Segui l’esercitazione su [mappatura di un file CSV in XDM](../../../../ingestion/tutorials/map-a-csv-file.md) per scoprire come convertire i campi dati in XDM e trasferirli in Platform. Quando selezioni [!UICONTROL Destinazione] per la mappatura, accertati di selezionare il **[!UICONTROL Utilizza set di dati esistenti]** e scegli la [!DNL Profile]Set di dati di consenso abilitato creato in precedenza.

## Verificare l’implementazione {#test-implementation}

Dopo aver acquisito i dati di consenso dei clienti nella [!DNL Profile]Set di dati abilitato, puoi controllare i profili aggiornati per verificare se contengono attributi di consenso.

>[!IMPORTANT]
>
>Per visualizzare gli attributi di un profilo esistente nell’interfaccia utente, devi conoscere almeno un valore di identità (e il relativo namespace) associato a tale profilo.
>
>Se non hai accesso a queste informazioni, puoi scegliere di acquisire i dati di consenso per il test e associarli a un valore o a uno spazio dei nomi di identità che ti è noto.

Vedi la sezione su [esplorazione dei profili per identità](../../../../profile/ui/user-guide.md#browse) in [!DNL Profile] Guida all’interfaccia utente per passaggi specifici su come cercare i dettagli di un profilo.

Per impostazione predefinita, i nuovi attributi di consenso non verranno visualizzati sul dashboard di un profilo. Pertanto, devi passare alla **[!UICONTROL Attributi]** nella pagina dei dettagli di un profilo per confermare che è stato acquisito come previsto. Consulta la guida [dashboard del profilo](../../../../profile/ui/profile-dashboard.md) per scoprire come personalizzare il dashboard in base alle proprie esigenze.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Passaggi successivi

Questa guida illustra come configurare le operazioni di Platform per elaborare i dati di consenso dei clienti utilizzando lo standard Adobe e far sì che tali attributi siano rappresentati nei profili dei clienti. È ora possibile integrare le preferenze di consenso dei clienti come fattore determinante nella qualificazione dei segmenti e in altri casi di utilizzo a valle.

Per ulteriori informazioni sulle funzionalità relative alla privacy di Experience Platform, consulta la panoramica su [governance, privacy e sicurezza in Platform](../../overview.md).
