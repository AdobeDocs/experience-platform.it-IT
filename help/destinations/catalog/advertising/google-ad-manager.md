---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connessione Google Ad Manager
description: Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci pubblicitari sui loro siti web, attraverso video e nelle app mobili.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 4df2e7ce9c7e94da4ea0be50ba21232c639e2587
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# [!DNL Google Ad Manager] connection

## Panoramica {#overview}

[!DNL Google Ad Manager], precedentemente noto come  [!DNL DoubleClick for Publishers] (DFP) o  [!DNL DoubleClick AdX], è una piattaforma di ad serving  [!DNL Google] che offre agli editori i mezzi per gestire la visualizzazione di annunci pubblicitari sui loro siti web, tramite video e nelle app mobili.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici delle destinazioni [!DNL Google Ad Manager]:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma [!DNL Google] .
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come  [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | ID pubblicità Microsoft. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

## Tipo di esportazione {#export-type}

**Esportazione segmento** : stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google.

## Prerequisiti

Se stai cercando di creare la tua prima destinazione con [!DNL Google Ad Manager] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Audience Manager o altre applicazioni), contatta la Consulenza di Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza avevi impostato le integrazioni [!DNL Google] in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Elenco consentiti

>[!NOTE]
>
>L’elenco consentiti è obbligatorio prima di configurare la tua prima destinazione [!DNL Google Ad Manager] in Platform. Prima di creare una destinazione, assicurati che il processo di elenco consentiti descritto di seguito sia stato completato da [!DNL Google].

Prima di creare la destinazione [!DNL Google Ad Manager] in Platform, è necessario contattare [!DNL Google] per Adobe per essere inserito nell’elenco dei provider di dati consentiti e per aggiungere l’account all’elenco consentiti. Contatta [!DNL Google] e fornisci le seguenti informazioni:

* **ID**  account: questo è l&#39;ID account di Adobe con  [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID**  cliente: questo è l&#39;ID account cliente Adobe con  [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID**  di rete: questo è il tuo account con  [!DNL Google Ad Manager]
* **ID**  collegamento pubblico: questo è il tuo account con  [!DNL Google Ad Manager]
* Tipo di account. DFP di Google o dell&#39;acquirente AdX.

## Configurare la destinazione

In **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, selezionare **[!DNL Google Ad Manager]** e selezionare **[!UICONTROL Configura]**.

![Connetti destinazione Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Attiva]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Attiva]** e **[!UICONTROL Configura]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila [!UICONTROL Informazioni di base] per la destinazione.

![Informazioni di base Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Tipo]** account: Seleziona un’opzione, a seconda del tuo account con Google:
   * Utilizza `DFP by Google` per [!DNL DoubleClick] per gli editori
   * Utilizza `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL ID]** account: Compila il tuo ID account con  [!DNL Google]. Può essere l&#39;ID di rete o l&#39;ID del collegamento di pubblico. In genere si tratta di un ID a otto cifre.
* **[!UICONTROL Azione]** di marketing: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Quando imposti una destinazione [!DNL Google Ad Manager], rivolgiti al tuo [!DNL Google Account Manager] o rappresentante di Adobe per capire quale tipo di account hai.

## Attiva i segmenti in [!DNL Google Ad Manager]

Per istruzioni su come attivare i segmenti su [!DNL Google Ad Manager], consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Ad Manager], controlla il tuo account [!DNL Google Ad Manager]. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
