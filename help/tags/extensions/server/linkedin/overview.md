---
title: Estensione di inoltro eventi API LinkedIn Conversions
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform consente di misurare le prestazioni della campagna di marketing LinkedIn.
last-substantial-update: 2023-10-25T00:00:00Z
source-git-commit: e1ed18aa79abae70974df1845c211a00390ecca4
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 2%

---

# Estensione API Conversions [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) è uno strumento di tracciamento della conversione che crea una connessione diretta tra i dati di marketing provenienti dal server dell’inserzionista e [!DNL LinkedIn]. Ciò consente agli inserzionisti di valutare l’efficacia della [!DNL LinkedIn] campagne di marketing indipendentemente dalla posizione della conversione e utilizza queste informazioni per promuovere l’ottimizzazione della campagna. Il [!DNL LinkedIn Conversions API] l’estensione può contribuire a rafforzare le prestazioni e a ridurre i costi per azione con un’attribuzione più completa, una maggiore affidabilità dei dati e una distribuzione ottimizzata.

## Prerequisiti {#prerequisites}

Devi creare una regola di conversione nel [!DNL LinkedIn] account degli annunci di campaign. [!DNL Adobe] consiglia di includere &quot;CAPI&quot; all’inizio del nome della regola di conversazione per distinguerlo dagli altri tipi di regole di conversione che potrebbero essere stati configurati.

### Creare un segreto e un elemento dati

Crea un nuovo [!DNL LinkedIn] [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md) e fornisci un nome univoco che indichi il membro che esegue l’autenticazione. Verrà utilizzato per autenticare la connessione al tuo account mantenendo protetto il valore.

Avanti, [creare un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando [!UICONTROL Core] e un [!UICONTROL Segreto] tipo di elemento dati per fare riferimento a `LinkedIn` segreto appena creato.

## Installare e configurare [!DNL LinkedIn] estensione {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) oppure seleziona una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona la scheda **[!UICONTROL LinkedIn]** e quindi seleziona **[!UICONTROL Installa]**.

![Il catalogo delle estensioni che mostra [!DNL LinkedIn] scheda dell&#39;estensione che evidenzia install.](../../../images/extensions/server/linkedin/install-extension.png)

Nella schermata successiva, immetti il segreto dell&#39;elemento dati creato in precedenza in `Access Token` campo. Il segreto dell’elemento dati conterrà i [!DNL LinkedIn] Token OAuth 2. Al termine, seleziona **[!UICONTROL Salva]**.

![Il [!DNL LinkedIn] pagina di configurazione dell&#39;estensione con [!UICONTROL Token di accesso] campo e [!UICONTROL Salva] evidenziato.](../../../images/extensions/server/linkedin/configure-extension.png)

## Creare un [!DNL Send Conversion] regola {#tracking-rule}

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro degli eventi che determinano quando e come verranno inviati gli eventi a [!DNL LinkedIn].

Crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro degli eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL LinkedIn]**. Quindi, seleziona **[!UICONTROL Invia conversione web]** per **[!UICONTROL Tipo di azione]**.

![La vista Regole proprietà inoltro eventi, con i campi necessari per aggiungere una configurazione dell’azione della regola di inoltro eventi evidenziati.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Dopo la selezione, vengono visualizzati controlli aggiuntivi per configurare ulteriormente l’evento. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la regola.

**[!UICONTROL Dati utente]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL E-mail] | Indirizzo e-mail del contatto associato all’evento di conversione. Il valore e-mail verrà codificato dal codice di estensione in SHA256, a meno che il valore fornito non sia già una stringa SHA256. |
| [!UICONTROL UUID tracciamento annunci prime parti di linkedIn] | Questo è un ID cookie di prima parte. Gli inserzionisti devono abilitare il tracciamento avanzato delle conversioni da [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) per attivare i cookie di prima parte che aggiungono un parametro ID clic `li_fat_id` agli URL di clic. |
| [!UICONTROL Dati informazioni cliente] | Questo campo contiene un oggetto JSON con attributi aggiuntivi che verranno inviati insieme al messaggio.<br><br>Sotto **[!UICONTROL Raw]** , puoi incollare l’oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l’icona dell’elemento dati (![Icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per scegliere da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. I valori chiave accettati sono: `firstName`, `lastName`, `companyName`, `title` e `country`. |

{style="table-layout:auto"}

![Il [!DNL User Data] mostra dati di esempio inseriti nei campi.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Dati di conversione]**

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Conversione] | ID della regola di conversione creata in [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) o attraverso [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL Tempo di conversione] | Ogni timestamp in millisecondi in cui si è verificato l’evento di conversione. <br><br> Nota: se l’origine registra il timestamp di conversione in secondi, inserisci 000 alla fine per trasformarlo in millisecondi. |
| [!UICONTROL Valuta] | Codice valuta in formato ISO. |
| [!UICONTROL Quantità] | Valore della conversione in stringa decimale (ad esempio, &quot;100.05&quot;). |
| [!UICONTROL ID evento] | L’ID univoco generato dagli inserzionisti per indicare ogni evento. Questo è un campo facoltativo e viene utilizzato per la deduplicazione. |

{style="table-layout:auto"}

![Il [!DNL Conversion Data] mostra dati di esempio nei campi.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Sostituzioni configurazione]**

>NOTA
>
>Il [!UICONTROL Sostituzioni configurazione] consente a un utente di impostare un diverso [!DNL LinkedIn] token di accesso su ogni regola, consentendo a ogni regola di utilizzare un token di accesso che può avere accesso a diversi [!DNL LinkedIn] ad account.

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Token di accesso] | Il [!DNL LinkedIn] token di accesso. |

![Il [!DNL Configuration Overrides] sezione che mostra dati di esempio immessi nel campo.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL LinkedIn] utilizzando [!DNL LinkedIn Conversions API] estensione di inoltro degli eventi. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in [!DNL Adobe Experience Platform], fare riferimento a [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).
