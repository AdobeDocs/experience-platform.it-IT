---
title: (Aziende) LinkedIn connection
description: Utilizza questa destinazione per attivare i tipi di pubblico di account per i casi d’uso di Account-Based Marketing (ABM). Attiva profili per le campagne LinkedIn per il targeting, la personalizzazione e l’eliminazione del pubblico, in base alle e-mail con hash.
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: 044306709747c32c4ce265d03d3908bbae169edc
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 6%

---

# (Aziende) LinkedIn - Corrispondenza tipi di pubblico connessione {#companies-linkedin}

>[!AVAILABILITY]
>
>La funzionalità per attivare i tipi di pubblico dell&#39;account nella destinazione LinkedIn (Aziende) è disponibile per le aziende che acquistano le edizioni [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) di Real-Time Customer Data Platform.

Utilizza questa destinazione per attivare i [tipi di pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) per i casi d&#39;uso di Account-Based Marketing (ABM). Pubblicizza a utenti tipo e ruoli rilevanti negli account di destinazione tramite la destinazione business-to-business **[!UICONTROL (Companies) LinkedIn]**. Visita la documentazione di LinkedIn per [ulteriori informazioni sul targeting degli account](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) sulla piattaforma LinkedIn.

>[!TIP]
>
>Per casi d&#39;uso a livello individuale (o business-to-consumer), Adobe consiglia di utilizzare la destinazione [Pubblico collegato](/help/destinations/catalog/social/linkedin.md).

![Destinazione account LinkedIn visualizzata nell&#39;interfaccia utente di Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importati](../../../segmentation/ui/overview.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-and-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|--------------|-----------|---------------------------|
| Tipo di esportazione | Esportazione pubblico | Tutti i membri del pubblico verranno esportati con identificatori chiave come nome, numero di telefono e altro ancora. |
| Frequenza | Streaming | Connessioni basate su API sempre attive. Gli aggiornamenti vengono inviati a valle immediatamente dopo le modifiche al profilo. |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per esportare i tipi di pubblico dell’account in LinkedIn, assicurati di soddisfare i prerequisiti seguenti:

### Prerequisiti per l&#39;account LinkedIn {#LinkedIn-account-prerequisites}

Prima di poter utilizzare la destinazione [!UICONTROL (Companies) LinkedIn Matched Audience], verificare che l&#39;account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le autorizzazioni utente di [!DNL LinkedIn Campaign Manager], consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione di controllo di accesso **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [&#128279;](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

1. Trovare la destinazione [!DNL (Companies) LinkedIn Matched Audiences] nel catalogo di destinazione e selezionare **[!UICONTROL Set Up]**.
2. Seleziona **[!UICONTROL Connect to destination]**.
   ![Autentica in LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Immetti le credenziali di LinkedIn e seleziona **Accedi**.

Dopo aver completato il processo di accesso con LinkedIn, puoi procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID nel tuo account [!DNL LinkedIn Campaign Manager].

Ora puoi attivare i tipi di pubblico dell’account su LinkedIn.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selezionare lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attiva pubblico account](/help/destinations/ui/activate-account-audiences.md) per le istruzioni sull&#39;attivazione del pubblico account in questa destinazione.

## Coppie di mappatura richieste nel passaggio di mappatura quando si attivano i tipi di pubblico dell&#39;account nella destinazione **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Quando si attivano i tipi di pubblico dell&#39;account nella destinazione **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, tenere presente che le due coppie di mappatura seguenti sono obbligatorie per esportare correttamente i dati:

![Mappatura campi obbligatori LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo di origine | Campo di destinazione |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (seleziona questo campo nella visualizzazione **[!UICONTROL Select Identity namespace]**, quando selezioni **[!UICONTROL Target Field]**). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selezionare lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico dell&#39;account nelle destinazioni."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Dati esportati {#exported-data}

Se l&#39;attivazione è riuscita, un pubblico personalizzato [!DNL LinkedIn] viene creato a livello di programmazione in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’iscrizione al pubblico viene regolata quando gli utenti vengono qualificati o squalificati per il pubblico attivato.
