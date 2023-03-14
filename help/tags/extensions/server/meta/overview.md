---
title: Panoramica dell’estensione API Meta Conversions
description: Scopri l’estensione API Meta Conversions per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---

# [!DNL Meta Conversions API] panoramica dell’estensione

Il [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) ti consente di collegare i dati di marketing lato server a [!DNL Meta] tecnologie per ottimizzare il targeting degli annunci, ridurre i costi per azione e misurare i risultati. Gli eventi sono collegati a un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID e vengono elaborati in modo simile agli eventi lato client.

Utilizzo di [!DNL Meta Conversions API] , puoi sfruttare le funzionalità dell&#39;API nella tua [inoltro eventi](../../../ui/event-forwarding/overview.md) regole a cui inviare i dati [!DNL Meta] dalla rete Edge di Adobe Experience Platform. Questo documento illustra come installare l’estensione e utilizzarne le funzionalità in un inoltro di eventi [regola](../../../ui/managing-resources/rules.md).

## Prerequisiti

Si consiglia vivamente di utilizzare [!DNL Meta Pixel] e [!DNL Conversions API] per condividere e inviare gli stessi eventi rispettivamente dal lato client e dal lato server, in quanto ciò può aiutare a recuperare eventi che non sono stati raccolti da [!DNL Meta Pixel]. Prima di installare [!DNL Conversions API] , consulta la guida sulla [[!DNL Meta Pixel] estensione](../../client/meta/overview.md) per i passaggi su come integrarlo nelle implementazioni tag lato client.

>[!NOTE]
>
>La sezione su [deduplicazione degli eventi](#deduplication) più avanti in questo documento vengono descritti i passaggi per garantire che lo stesso evento non venga utilizzato due volte, in quanto può essere ricevuto sia dal browser che dal server.

Per utilizzare il [!DNL Conversions API] , devi avere accesso all&#39;inoltro degli eventi e disporre di un [!DNL Meta] account con accesso a [!DNL Ad Manager] e [!DNL Event Manager]. In particolare, devi copiare l’ID di un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (o [crea un nuovo [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) in modo che l’estensione possa essere configurata sul tuo account.

## Installare l’estensione

Per installare [!DNL Meta Conversions API] , passa all’interfaccia utente di Data Collection o all’interfaccia utente di Experience Platform e seleziona **[!UICONTROL Inoltro eventi]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Catalogo]** scheda. Cerca [!UICONTROL API di metaconversione] , quindi seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Installa] pulsante selezionato per il [!UICONTROL API di metaconversione] nell’interfaccia utente di Data Collection.](../../../images/extensions/server/meta/install.png)

Nella vista di configurazione visualizzata, devi fornire [!DNL Pixel] ID copiato in precedenza per collegare l&#39;estensione al tuo account. Puoi incollare l’ID direttamente nell’input, oppure puoi utilizzare un elemento dati.

È inoltre necessario fornire un token di accesso per utilizzare [!DNL Conversions API] in particolare. Consulta la sezione [!DNL Conversions API] documentazione su [generazione di un token di accesso](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) per i passaggi su come ottenere questo valore.

Al termine, seleziona **[!UICONTROL Salva]**

![Il [!DNL Pixel] ID fornito come elemento dati nella vista di configurazione dell’estensione.](../../../images/extensions/server/meta/configure.png)

L&#39;estensione è installata e ora puoi utilizzarne le funzionalità nelle regole di inoltro degli eventi.

## Configurare una regola di inoltro degli eventi {#rule}

Questa sezione descrive come utilizzare [!DNL Conversions API] estensione in una regola di inoltro eventi generica. In pratica, devi configurare diverse regole per inviare tutti gli elementi accettati [eventi standard](https://developers.facebook.com/docs/meta-pixel/reference) tramite [!DNL Meta Pixel] e [!DNL Conversions API].

>[!NOTE]
>
>Gli eventi devono essere [inviato in tempo reale](https://www.facebook.com/business/help/379226453470947?id=818859032317965) o il più vicino possibile al tempo reale per ottimizzare le campagne pubblicitarie.

Inizia a creare una nuova regola di inoltro degli eventi e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Estensione API per metaconversione]** per l’estensione, seleziona **[!UICONTROL Evento API di invio conversioni]** per il tipo di azione.

![Il [!UICONTROL Invia visualizzazione pagina] tipo di azione selezionato per una regola nell’interfaccia utente di Data Collection.](../../../images/extensions/server/meta/select-action.png)

Vengono visualizzati i controlli che consentono di configurare i dati evento che verranno inviati a [!DNL Meta] tramite [!DNL Conversions API]. Queste opzioni possono essere immesse direttamente negli input forniti, oppure puoi selezionare elementi dati esistenti per rappresentare i valori. Le opzioni di configurazione sono suddivise in quattro sezioni principali, come descritto di seguito.

| Sezione di configurazione | Descrizione |
| --- | --- |
| [!UICONTROL Parametri evento server] | Informazioni generali sull&#39;evento, tra cui l&#39;ora in cui si è verificato e l&#39;azione di origine che l&#39;ha attivato. Consulta la sezione [!DNL Meta] documentazione per gli sviluppatori di per ulteriori informazioni su [parametri evento standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) accettata dal [!DNL Conversions API].<br><br>Se utilizzi entrambi [!DNL Meta Pixel] e [!DNL Conversions API] per inviare gli eventi, assicurati di includere sia un **[!UICONTROL Nome evento]** (`event_name`) e **[!UICONTROL ID evento]** (`event_id`) con ogni evento, poiché questi valori vengono utilizzati per [deduplicazione degli eventi](#deduplication).<br><br>È inoltre possibile: **[!UICONTROL Abilita utilizzo dati limitato]** per rispettare le rinunce dei clienti. Consulta la [!DNL Conversions API] documentazione su [opzioni di elaborazione dati](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) per i dettagli su questa funzione. |
| [!UICONTROL Parametri informazioni cliente] | Dati di identità utente utilizzati per attribuire l’evento a un cliente. Per poter essere inviati all&#39;API, alcuni di questi valori devono avere un hash.<br><br>Per garantire una buona connessione API in comune e un’elevata qualità di corrispondenza degli eventi (EMQ), si consiglia di inviare tutti [parametri accettati per le informazioni sul cliente](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) insieme agli eventi del server. Anche questi parametri devono essere [prioritario in base alla loro importanza e impatto su EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Dati personalizzati] | Dati aggiuntivi da utilizzare per l’ottimizzazione della consegna di annunci, forniti sotto forma di oggetto JSON. Consulta la sezione [[!DNL Conversions API] documentazione](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) per ulteriori informazioni sulle proprietà accettate per questo oggetto.<br><br>Se invii un evento di acquisto, devi utilizzare questa sezione per fornire gli attributi richiesti `currency` e `value`. |
| [!UICONTROL Evento di test] | Questa opzione viene utilizzata per verificare se la configurazione causa la ricezione di eventi server da parte di [!DNL Meta] come previsto. Per utilizzare questa funzione, selezionare **[!UICONTROL Invia come evento di test]** e quindi inserisci il codice di un evento di test desiderato nell’input seguente. Una volta distribuita la regola di inoltro degli eventi, se hai configurato correttamente l’estensione e l’azione dovresti visualizzare le attività presenti all’interno di **[!DNL Test Events]** visualizza in [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Al termine, seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola.

![[!UICONTROL Mantieni modifiche] in fase di selezione per la configurazione dell’azione.](../../../images/extensions/server/meta/keep-changes.png)

Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**. Infine, pubblica un nuovo inoltro di eventi [build](../../../ui/publishing/builds.md) per abilitare le modifiche apportate alla libreria.

## Deduplicazione di eventi {#deduplication}

Come indicato nella [sezione prerequisiti](#prerequisites), si consiglia di utilizzare entrambi i [!DNL Meta Pixel] estensione tag e [!DNL Conversions API] estensione di inoltro degli eventi per inviare gli stessi eventi dal client e dal server in una configurazione ridondante. Questo può aiutare a recuperare gli eventi che non sono stati rilevati da un’estensione o dall’altra.

Se invii tipi di evento diversi dal client e dal server senza alcuna sovrapposizione tra i due, la deduplicazione non è necessaria. Tuttavia, se un singolo evento è condiviso da entrambi [!DNL Meta Pixel] e [!DNL Conversions API], è necessario assicurarsi che questi eventi ridondanti siano deduplicati in modo che il reporting non venga influenzato negativamente.

Quando invii eventi condivisi, accertati di includere un ID evento e un nome con ogni evento inviato sia dal client che dal server. Quando si ricevono più eventi con lo stesso ID e nome, [!DNL Meta] utilizza automaticamente diverse strategie per deduplicarle e conservare i dati più rilevanti. Consulta la [!DNL Meta] documentazione su [deduplicazione per [!DNL Meta Pixel] e [!DNL Conversions API] Eventi](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) per informazioni dettagliate su questo processo.

## Passaggi successivi

Questa guida illustra come inviare dati evento lato server a [!DNL Meta] utilizzando [!DNL Meta Conversions API] estensione. Da qui, si consiglia di espandere la tua integrazione collegando più [!DNL Pixels] e la condivisione di altri eventi, se applicabile. Effettuando una delle seguenti operazioni puoi migliorare ulteriormente le prestazioni dell’annuncio:

* Connetti qualsiasi altro [!DNL Pixels] che non sono ancora connessi a un [!DNL Conversions API] integrazione.
* Se invii determinati eventi esclusivamente tramite [!DNL Meta Pixel] sul lato client, invia gli stessi eventi al [!DNL Conversions API] anche dal lato server.

Consulta la [!DNL Meta] documentazione su [best practice per [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) per maggiori informazioni su come implementare in modo efficace l’integrazione. Per informazioni più generali sui tag e sull’inoltro di eventi in Adobe Experience Cloud, consulta [panoramica sui tag](../../../home.md).
