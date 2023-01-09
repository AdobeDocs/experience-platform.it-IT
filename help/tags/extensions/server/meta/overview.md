---
title: Panoramica dell’estensione API per le metaconversioni
description: Scopri l’estensione API Meta Conversions per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 0%

---

# [!DNL Meta Conversions API] panoramica dell&#39;estensione

La [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) consente di collegare i dati di marketing lato server a [!DNL Meta] tecnologie per ottimizzare il targeting degli annunci, ridurre il costo per azione e misurare i risultati. Gli eventi sono collegati a un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID e vengono elaborati in modo simile agli eventi lato client.

Utilizzo della [!DNL Meta Conversions API] puoi sfruttare le funzionalità dell&#39;API nel [inoltro eventi](../../../ui/event-forwarding/overview.md) regole a cui inviare i dati [!DNL Meta] da Adobe Experience Platform Edge Network. Questo documento illustra come installare l&#39;estensione e utilizzarne le funzionalità in un inoltro eventi [regola](../../../ui/managing-resources/rules.md).

## Prerequisiti

Si consiglia vivamente di utilizzare [!DNL Meta Pixel] e [!DNL Conversions API] per condividere e inviare gli stessi eventi dal lato client e dal lato server, rispettivamente, in quanto ciò potrebbe aiutare a recuperare gli eventi che non sono stati rilevati da [!DNL Meta Pixel]. Prima di installare [!DNL Conversions API] estensione, consulta la guida [[!DNL Meta Pixel] estensione](../../client/meta/overview.md) per i passaggi su come integrarlo nelle implementazioni di tag lato client.

>[!NOTE]
>
>La sezione [deduplicazione degli eventi](#deduplication) più avanti in questo documento descrive i passaggi per garantire che lo stesso evento non venga utilizzato due volte, in quanto può essere ricevuto sia dal browser che dal server.

Per utilizzare il [!DNL Conversions API] estensione, devi disporre dell&#39;accesso all&#39;inoltro eventi e avere una valida [!DNL Meta] account con accesso a [!DNL Ad Manager] e [!DNL Event Manager]. In particolare, devi copiare l’ID di un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) o [creare una nuova [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) in questo modo l&#39;estensione può essere configurata sul tuo account.

## Installare l’estensione

Per installare [!DNL Meta Conversions API] , passa all’interfaccia utente di raccolta dati o di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dalla navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Catalogo]** scheda . Cerca il [!UICONTROL API per le metaconversioni] scheda , quindi seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Installa] pulsante selezionato per [!UICONTROL API per le metaconversioni] estensione nell’interfaccia utente di raccolta dati.](../../../images/extensions/server/meta/install.png)

Nella visualizzazione di configurazione visualizzata, devi fornire [!DNL Pixel] ID copiato in precedenza per collegare l&#39;estensione al tuo account . Puoi incollare l’ID direttamente nell’input, oppure puoi utilizzare un elemento dati.

È inoltre necessario fornire un token di accesso per utilizzare il [!DNL Conversions API] specificamente. Fai riferimento a [!DNL Conversions API] documentazione [generazione di un token di accesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) per i passaggi su come ottenere questo valore.

Al termine, seleziona **[!UICONTROL Salva]**

![La [!DNL Pixel] ID fornito come elemento dati nella visualizzazione di configurazione dell&#39;estensione.](../../../images/extensions/server/meta/configure.png)

L&#39;estensione è installata e ora puoi utilizzarne le funzionalità nelle regole di inoltro degli eventi.

## Configurare una regola di inoltro eventi {#rule}

Questa sezione descrive come utilizzare il [!DNL Conversions API] estensione in una regola di inoltro eventi generica. In pratica, devi configurare diverse regole per inviare tutte le regole accettate [eventi standard](https://developers.facebook.com/docs/meta-pixel/reference) tramite [!DNL Meta Pixel] e [!DNL Conversions API].

>[!NOTE]
>
>Eventi [inviato in tempo reale](https://www.facebook.com/business/help/379226453470947?id=818859032317965) o il più vicino possibile in tempo reale per una migliore ottimizzazione delle campagne pubblicitarie.

Inizia a creare una nuova regola di inoltro eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Estensione API Meta Conversioni]** per l&#39;estensione , quindi seleziona **[!UICONTROL Evento API di invio delle conversioni]** per il tipo di azione.

![La [!UICONTROL Invia visualizzazione pagina] tipo di azione selezionato per una regola nell&#39;interfaccia utente Raccolta dati.](../../../images/extensions/server/meta/select-action.png)

Vengono visualizzati i controlli che consentono di configurare i dati dell’evento a cui verranno inviati [!DNL Meta] tramite [!DNL Conversions API]. Queste opzioni possono essere immesse direttamente negli input forniti oppure è possibile selezionare elementi dati esistenti per rappresentare i valori. Le opzioni di configurazione sono suddivise in quattro sezioni principali come descritto di seguito.

| Sezione Configurazione | Descrizione |
| --- | --- |
| [!UICONTROL Parametri evento server] | Informazioni generali sull’evento, inclusa l’ora in cui si è verificato e l’azione sorgente che l’ha attivato. Fai riferimento a [!DNL Meta] documentazione per gli sviluppatori per ulteriori informazioni [parametri evento standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) accettati dalla [!DNL Conversions API].<br><br>Se utilizzi entrambi [!DNL Meta Pixel] e [!DNL Conversions API] per inviare eventi, assicurati di includere sia un **[!UICONTROL Nome evento]** (`event_name`) e **[!UICONTROL ID evento]** (`event_id`) per ogni evento, in quanto questi valori vengono utilizzati per [deduplicazione degli eventi](#deduplication).<br><br>Hai anche la possibilità di **[!UICONTROL Abilita uso limitato dei dati]** per rispettare le rinunce dei clienti. Consulta la sezione [!DNL Conversions API] documentazione [opzioni di elaborazione dati](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) per informazioni dettagliate su questa funzione. |
| [!UICONTROL Parametri di informazioni cliente] | Dati di identità utente utilizzati per attribuire l&#39;evento a un cliente. Per poter essere inviati all’API, è necessario eseguire un hash per alcuni di questi valori.<br><br>Per garantire una buona connessione API comune e un’elevata qualità di corrispondenza degli eventi (EMQ), si consiglia di inviare tutti [parametri accettati per le informazioni sui clienti](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) insieme agli eventi server. Questi parametri devono essere [priorità in base alla loro importanza e impatto su EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Dati personalizzati] | Dati aggiuntivi da utilizzare per l’ottimizzazione della distribuzione degli annunci, forniti sotto forma di un oggetto JSON. Fai riferimento a [[!DNL Conversions API] documentazione](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) per ulteriori informazioni sulle proprietà accettate per questo oggetto.<br><br>Se invii un evento di acquisto, devi utilizzare questa sezione per fornire gli attributi richiesti `currency` e `value`. |
| [!UICONTROL Evento di prova] | Questa opzione viene utilizzata per verificare se la configurazione causa la ricezione di eventi server da parte di [!DNL Meta] come previsto. Per utilizzare questa funzione, seleziona la **[!UICONTROL Invia come evento di prova]** , quindi fornisci un codice evento di prova desiderato nell’input seguente. Una volta distribuita la regola di inoltro eventi, se hai configurato correttamente l&#39;estensione e l&#39;azione dovresti vedere le attività che compaiono all&#39;interno della **[!DNL Test Events]** visualizza in [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola.

![[!UICONTROL Mantieni modifiche] selezionato per la configurazione dell&#39;azione.](../../../images/extensions/server/meta/keep-changes.png)

Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**. Infine, pubblica un nuovo inoltro evento [build](../../../ui/publishing/builds.md) per abilitare le modifiche apportate alla libreria.

## Deduplicazione di eventi {#deduplication}

Come indicato nella [sezione prerequisiti](#prerequisites), si consiglia di utilizzare sia la [!DNL Meta Pixel] l&#39;estensione del tag e [!DNL Conversions API] estensione dell&#39;inoltro eventi per inviare gli stessi eventi dal client e dal server in una configurazione ridondante. Questo può aiutare a recuperare gli eventi che non sono stati rilevati da un&#39;estensione o dall&#39;altra.

Se invii tipi di evento diversi dal client e dal server senza sovrapposizione tra i due, la deduplicazione non è necessaria. Tuttavia, se un singolo evento è condiviso da entrambi [!DNL Meta Pixel] e [!DNL Conversions API], devi assicurarti che questi eventi ridondanti siano deduplicati in modo che la generazione di rapporti non subisca effetti negativi.

Quando invii eventi condivisi, assicurati di includere un ID evento e un nome con ogni evento inviato dal client e dal server. Quando vengono ricevuti più eventi con lo stesso ID e lo stesso nome, [!DNL Meta] utilizza automaticamente diverse strategie per deduplicarle e conservare i dati più rilevanti. Consulta la sezione [!DNL Meta] documentazione [deduplicazione per [!DNL Meta Pixel] e [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) per informazioni dettagliate su questo processo.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL Meta] utilizzando [!DNL Meta Conversions API] estensione. Da qui, è consigliabile espandere l’integrazione connettendo altre opzioni [!DNL Pixels] e condividere altri eventi, se applicabile. Effettuare una delle seguenti operazioni può migliorare ulteriormente le prestazioni dell&#39;annuncio:

* Connetti a qualsiasi altro [!DNL Pixels] che non sono ancora collegati a un [!DNL Conversions API] integrazione.
* Se invii determinati eventi esclusivamente tramite [!DNL Meta Pixel] sul lato client, invia gli stessi eventi al [!DNL Conversions API] anche dal lato server.

Consulta la sezione [!DNL Meta] documentazione [best practice per [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) per ulteriori informazioni su come implementare efficacemente l’integrazione. Per informazioni più generali sui tag e sull&#39;inoltro degli eventi in Adobe Experience Cloud, consulta [panoramica dei tag](../../../home.md).
