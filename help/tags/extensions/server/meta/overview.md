---
title: Panoramica dell’estensione API per le metaconversioni
description: Scopri l’estensione API Meta Conversions per l’inoltro di eventi in Adobe Experience Platform.
source-git-commit: a47e35a1b8c7ce2b0fa4ffe30fcdc7d22fc0f4c5
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# [!DNL Meta Conversions API] panoramica dell&#39;estensione

La [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) consente di collegare i dati di marketing lato server a [!DNL Meta] tecnologie per ottimizzare il targeting degli annunci, ridurre il costo per azione e misurare i risultati. Gli eventi sono collegati a un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID e vengono elaborati in modo simile agli eventi lato client.

Utilizzo della [!DNL Meta Conversions API] puoi sfruttare le funzionalità dell&#39;API nel [inoltro eventi](../../../ui/event-forwarding/overview.md) regole a cui inviare i dati [!DNL Meta] da Adobe Experience Platform Edge Network. Questo documento illustra come installare l&#39;estensione e utilizzarne le funzionalità in un inoltro eventi [regola](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Se stai tentando di inviare eventi a [!DNL Meta] dal lato client anziché dal lato server, utilizza il [[!DNL Meta Pixiel] estensione tag](../../client/meta/overview.md) invece.

## Prerequisiti

Per utilizzare l&#39;estensione, devi accedere all&#39;inoltro eventi e disporre di un [!DNL Meta] account con accesso a [!DNL Ad Manager] e [!DNL Event Manager]. In particolare, devi copiare l’ID di un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) o [creare una nuova [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) in questo modo l&#39;estensione può essere configurata sul tuo account.

## Installare l’estensione

Per installare [!DNL Meta Conversions API] , passa all’interfaccia utente di raccolta dati o di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dalla navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Catalogo]** scheda . Cerca il [!UICONTROL API per le metaconversioni] scheda , quindi seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Installa] pulsante selezionato per [!UICONTROL API per le metaconversioni] estensione nell’interfaccia utente di raccolta dati.](../../../images/extensions/server/meta/install.png)

Nella visualizzazione di configurazione visualizzata, devi fornire [!DNL Pixel] ID copiato in precedenza per collegare l&#39;estensione al tuo account . Puoi incollare l’ID direttamente nell’input, oppure puoi utilizzare un elemento dati.

È inoltre necessario fornire un token di accesso per utilizzare il [!DNL Conversions API] specificamente. Fai riferimento a [!DNL Conversions API] documentazione [generazione di un token di accesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) per i passaggi su come ottenere questo valore.

Al termine, seleziona **[!UICONTROL Salva]**

![La [!DNL Pixel] ID fornito come elemento dati nella visualizzazione di configurazione dell&#39;estensione.](../../../images/extensions/server/meta/configure.png)

L&#39;estensione è installata e ora puoi utilizzarne le funzionalità nelle regole dei tag.

## Configurare una regola di inoltro eventi {#rule}

Inizia a creare una nuova regola di inoltro eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Estensione API Meta Conversioni]** per l&#39;estensione , quindi seleziona **[!UICONTROL Evento API di invio delle conversioni]** per il tipo di azione.

![La [!UICONTROL Invia visualizzazione pagina] tipo di azione selezionato per una regola nell&#39;interfaccia utente Raccolta dati.](../../../images/extensions/server/meta/select-action.png)

Vengono visualizzati i controlli che consentono di configurare i dati dell’evento a cui verranno inviati [!DNL Meta] tramite [!DNL Conversions API]. Queste opzioni possono essere immesse direttamente negli input forniti oppure è possibile selezionare elementi dati esistenti per rappresentare i valori. Le opzioni di configurazione sono suddivise in quattro sezioni principali come descritto di seguito.

| Sezione Configurazione | Descrizione |
| --- | --- |
| [!UICONTROL Parametri evento server] | Informazioni generali sull’evento, inclusa l’ora in cui si è verificato e l’azione sorgente che l’ha attivato. Fai riferimento a [[!DNL Conversions API] documentazione](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) per ulteriori informazioni su questi parametri.<br><br>Hai anche la possibilità di **[!UICONTROL Abilita uso limitato dei dati]** per rispettare le rinunce dei clienti. Consulta la sezione [!DNL Conversions API] documentazione [opzioni di elaborazione dati](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) per informazioni dettagliate su questa funzione. |
| [!UICONTROL Parametri di informazioni cliente] | Dati di identità utente utilizzati per attribuire l&#39;evento a un cliente. Per poter essere inviati all’API, è necessario eseguire un hash per alcuni di questi valori. Fai riferimento a [[!DNL Conversions API] documentazione](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) per ulteriori informazioni su questi parametri. |
| [!UICONTROL Dati personalizzati] | Dati aggiuntivi da utilizzare per l’ottimizzazione della distribuzione degli annunci, forniti sotto forma di un oggetto JSON. Fai riferimento a [[!DNL Conversions API] documentazione](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) per ulteriori informazioni sulle proprietà accettate per questo oggetto.<br><br>Se invii un evento di acquisto, devi utilizzare questa sezione per fornire gli attributi richiesti `currency` e `value`. |
| [!UICONTROL Evento di prova] | Questa opzione viene utilizzata per verificare se la configurazione causa la ricezione di eventi server da parte di [!DNL Meta] come previsto. Per utilizzare questa funzione, seleziona la **[!UICONTROL Invia come evento di prova]** , quindi fornisci un codice evento di prova desiderato nell’input seguente. Una volta distribuita la regola di inoltro eventi, se hai configurato correttamente l&#39;estensione e l&#39;azione dovresti vedere le attività che compaiono all&#39;interno della **[!DNL Test Events]** visualizza in [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola.

![[!UICONTROL Mantieni modifiche] selezionato per la configurazione dell&#39;azione.](../../../images/extensions/server/meta/keep-changes.png)

Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**. Infine, pubblica un nuovo inoltro evento [build](../../../ui/publishing/builds.md) per abilitare le modifiche apportate alla libreria.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL Meta] utilizzando [!DNL Meta Conversions API] estensione. Per ulteriori informazioni sui tag e sull’inoltro degli eventi, consulta la [panoramica dei tag](../../../home.md).
