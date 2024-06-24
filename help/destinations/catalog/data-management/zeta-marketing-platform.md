---
title: Zeta Marketing Platform
description: Zeta Marketing Platform (ZMP) è un sistema basato su cloud che consente di acquisire, crescere e mantenere i clienti in modo più efficiente, grazie all’intelligenza (dati proprietari e AI).
hide: true
hidefromtoc: true
source-git-commit: bf553371316d9d9cb368fc4d1be14196201ef680
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Zeta Marketing Platform {#zeta-marketing-platform}

## Panoramica {#overview}

Zeta Marketing Platform (ZMP) è un sistema basato su cloud che consente di acquisire, crescere e mantenere i clienti in modo più efficiente, grazie all’intelligenza (dati proprietari e AI). Per ulteriori informazioni, consulta [Zeta Global](https://zetaglobal.com/).

Con il connettore Zeta Marketing Platform disponibile in Adobe Experience Platform, puoi sincronizzare facilmente i tipi di pubblico da Experienci Platform a ZMP.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da *Zeta Global* team. Per richieste di informazioni o richieste di aggiornamento, contatta il team all’indirizzo [Contattaci](https://zetaglobal.com/about/contact-us/).

## Casi d’uso {#use-cases}

### Creare segmenti di pubblico {#use-case-build-audiences}

Un addetto al marketing vuole creare profili di pubblico univoci, identificare i segmenti più importanti e utilizzarli su tutti i canali digitali supportati dalla Zeta Marketing Platform. Desiderano creare una visualizzazione a 360 reali di un profilo di consumo, generare e attivare tipi di pubblico significativi. Ulteriori dettagli sui canali supportati da Zeta Marketing Platform sono disponibili [qui](https://zetaglobal.com/platform/integrations/).

### Eseguire il targeting degli utenti con annunci pubblicitari {#use-case-target-users}

Un inserzionista mira a indirizzare gli utenti all’interno di tipi di pubblico specifici tramite il Demand Side Platform Zeta (DSP), in quanto tali utenti interagiscono con i loro marchi. Per ulteriori informazioni sull’DSP Zeta, fai clic su [qui](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## Prerequisiti {#prerequisites}

### Prerequisiti per la piattaforma Zeta Marketing

* Prima di impostare una nuova connessione alla destinazione Zeta Marketing Platform, è necessario creare un elenco di clienti vuoto nell’account Zeta Marketing Platform. Devi scegliere uno di questi elenchi di clienti come destinazione designata per ricevere il pubblico Adobe Experience Platform che intendi inviare. Puoi creare un elenco clienti vuoto nello ZMP seguendo le istruzioni [qui](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Anche se Adobe Experience Platform consente l’attivazione di più tipi di pubblico a una particolare istanza di destinazione ZMP, è obbligatorio che ogni istanza di destinazione ZMP riceva un solo pubblico di Experience Platform. Per gestire più tipi di pubblico dall’Experience Platform, crea altre istanze di destinazione ZMP per ciascun pubblico e seleziona un elenco di clienti diverso dal menu a discesa. Questo approccio assicura che i tipi di pubblico ZMP di destinazione non vengano sovrascritti. Consulta [Inserisci i dettagli della destinazione](#destination-details) per ulteriori dettagli.
* Utilizza le seguenti credenziali per configurare la destinazione:
   * Nome utente: **api**
   * Password: la chiave API REST ZMP. Per trovare la chiave REST API, accedi al tuo account ZMP e passa a **Impostazioni** > **Integrazioni** > **Chiavi e app** sezione. Consulta la [Documentazione ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) per ulteriori dettagli.

## Identità supportate {#supported-identities}

[!DNL Zeta Marketing Platform] supporta l’attivazione degli ID utente personalizzati descritti nella tabella seguente. Per ulteriori dettagli, consulta [identità](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> La destinazione di Zeta Marketing Platform richiede di mappare uno spazio dei nomi dell’identità di origine allo ZMP `uid` identità di destinazione. Questo aiuta la Zeta Marketing Platform a differenziare in modo univoco ogni profilo.

| Identità di destinazione | Descrizione | Considerazioni | Note |
---------|----------|----------|----------|
| uid | ID univoco utilizzato da ZMP per differenziare i profili dei clienti | Obbligatorio | Scegli la `Email` spazio dei nomi identità standard se desideri identificare profili univoci utilizzando i loro indirizzi e-mail. In alternativa, puoi scegliere di mappare lo spazio dei nomi personalizzato su `uid` se i profili cliente non hanno un messaggio e-mail. |
| email_md5_id | Invia un messaggio e-mail MD5 che rappresenta ogni profilo cliente | Facoltativo | Scegli questa identità di destinazione quando intendi identificare in modo univoco i profili dei clienti utilizzando i valori e-mail MD5. È essenziale che gli indirizzi e-mail siano già in formato MD5 nell’Experience Platform, in quanto Platform non converte il testo normale in MD5. In questo scenario, imposta `uid` (obbligatorio) agli stessi valori e-mail MD5 o a un altro spazio dei nomi di identità appropriato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

>[!NOTE]
> Man mano che i singoli membri vengono aggiunti o rimossi dal pubblico di Platform, gli aggiornamenti verranno inviati allo ZMP per garantire che l’elenco dei clienti di destinazione sia sincronizzato di conseguenza.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Nome utente]**: `api`
* **[!UICONTROL Password]**: la chiave API REST ZMP. Per trovare la chiave REST API, accedi al tuo account ZMP e passa a **Impostazioni** > **Integrazioni** > **Chiavi e app** sezione. Consulta la [Documentazione ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) per ulteriori dettagli.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Immagine che mostra la configurazione ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID sito account ZMP]**: ZMP **ID sito** dove desideri inviare i tipi di pubblico a. Per visualizzare l’ID sito, vai a **Impostazioni** > **Integrazioni** > **Chiavi e app** sezione. Ulteriori informazioni sono disponibili [qui](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL Segmento ZMP]**: il segmento dell’elenco clienti nell’account ID sito ZMP che desideri aggiornare con il pubblico di Platform.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Di seguito è riportato un esempio di corretta mappatura identità durante l’esportazione di profili in [!DNL Zeta Marketing Platform].

Selezione dei campi di origine:
* Seleziona uno spazio dei nomi dell’identità di origine (personalizzato o standard, ad esempio `Email`) che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL Zeta Marketing Platform].
* Seleziona gli attributi del profilo di origine XDM da esportare e aggiornare in [!DNL Zeta Marketing Platform].

Selezione dei campi di destinazione:
* (Obbligatorio) Seleziona `uid` come identità di destinazione a cui mappare uno spazio dei nomi dell’identità di origine.
* (Facoltativo) Seleziona `email_md5_id` come identità di destinazione in cui è stato mappato lo spazio dei nomi dell’identità di origine che rappresenta i valori e-mail md5. È essenziale che gli indirizzi e-mail siano già in formato MD5 nell’Experience Platform, in quanto Platform non converte il testo normale in MD5
* Se necessario, seleziona eventuali mappature di destinazione aggiuntive.

![Mappatura identità](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

In caso di esito positivo dell’attivazione del pubblico da Experienci Platform a Zeta Marketing Platform, viene aggiornato l’elenco dei clienti target in ZMP. Il conteggio e i profili di esempio nell’elenco dei clienti di destinazione saranno pari al numero di identità attivate correttamente.

![Elenco clienti in ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Ogni membro del pubblico attivato da Experienci Platform sarà visibile anche in **Tipi di pubblico** > **Persone** nello ZMP. Potrai anche visualizzare **Elenco clienti** un segmento a cui appartiene un profilo nella vista Cliente singolo, come illustrato di seguito.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

* [Knowledge Base di Zeta](https://knowledgebase.zetaglobal.com/zmp/)
