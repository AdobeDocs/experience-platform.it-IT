---
title: Panoramica dell’estensione Adobe Privacy
description: Scopri l’estensione tag Adobe Privacy in Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 9%

---

# Panoramica dell’estensione Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’estensione tag Adobe Privacy consente di raccogliere e rimuovere gli ID utente assegnati agli utenti finali dalle soluzioni Adobe sui dispositivi lato client. Gli ID raccolti possono quindi essere inviati a [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) per accedere o eliminare i dati personali dell&#39;individuo correlato nelle applicazioni Adobe Experience Cloud supportate.

Questa guida illustra come installare e configurare l’estensione Adobe Privacy nell’interfaccia utente di Experience Platform o nell’interfaccia utente di Data Collection.

>[!NOTE]
>
>Se preferisci installare queste funzionalità senza utilizzare i tag, consulta la [Panoramica sulla libreria JavaScript Privacy](../../../../privacy-service/js-library.md) per i passaggi su come implementare utilizzando il codice non elaborato.

## Installare e configurare l’estensione

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito dalla scheda **[!UICONTROL Catalogo]**. Utilizza la barra di ricerca per restringere l’elenco delle estensioni disponibili fino a individuare Adobe Privacy. Seleziona **[!UICONTROL Installa]** per continuare.

![Installa l&#39;estensione](../../../images/extensions/client/privacy/install.png)

La schermata successiva consente di configurare da quali origini e soluzioni desideri che l&#39;estensione raccolga gli ID. Le seguenti soluzioni sono supportate per l&#39;estensione:

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Servizio Adobe Experience Cloud Identity (Visitor o ECID)
* Adobe Advertising Cloud (AdCloud)

Seleziona una o più soluzioni, quindi seleziona **[!UICONTROL Aggiorna]**.

![Seleziona soluzioni](../../../images/extensions/client/privacy/select-solutions.png)

La schermata si aggiorna per mostrare gli input per i parametri di configurazione richiesti in base alle soluzioni selezionate.

![Proprietà richieste](../../../images/extensions/client/privacy/required-properties.png)

Utilizzando il menu a discesa sottostante, puoi anche aggiungere parametri aggiuntivi specifici della soluzione alla configurazione.

![Proprietà facoltative](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Per informazioni dettagliate sui valori di configurazione accettati per ciascuna soluzione supportata, vedere la sezione relativa ai [parametri di configurazione](../../../../privacy-service/js-library.md#config-params) nella panoramica della libreria JavaScript per la privacy.

Dopo aver aggiunto i parametri per le soluzioni selezionate, seleziona **[!UICONTROL Salva]** per salvare la configurazione.

![Proprietà facoltative](../../../images/extensions/client/privacy/save-config.png)

## Utilizzo dell’estensione {#using}

L&#39;estensione Adobe Privacy fornisce tre tipi di azione che possono essere utilizzati in una [regola](../../../ui/managing-resources/rules.md) quando si verifica un determinato evento e vengono soddisfatte le condizioni:

* **[!UICONTROL Recupera identità]**: le informazioni di identità memorizzate dell&#39;utente vengono recuperate.
* **[!UICONTROL Rimuovi identità]**: le informazioni di identità memorizzate dell&#39;utente sono state rimosse.
* **[!UICONTROL Recupera e rimuovi identità]**: le informazioni di identità memorizzate dell&#39;utente vengono recuperate e quindi rimosse.

Per ciascuna delle azioni di cui sopra, devi fornire una funzione di callback di JavaScript che accetti e gestisca i dati di identità recuperati come parametro di oggetto. Da qui è possibile archiviare queste identità, visualizzarle o inviarle all&#39;API [Privacy Service](../../../../privacy-service/api/overview.md) come richiesto.

Quando utilizzi l’estensione tag Adobe Privacy, devi fornire la funzione di callback richiesta sotto forma di un elemento dati. Consulta la sezione successiva per informazioni su come configurare questo elemento dati.

### Definire un elemento dati per gestire le identità

Avvia il processo di creazione di un nuovo elemento dati selezionando **[!UICONTROL Elementi dati]** nell&#39;area di navigazione a sinistra, seguito da **[!UICONTROL Aggiungi elemento dati]**. Nella schermata di configurazione, seleziona **[!UICONTROL Core]** per l&#39;estensione e **[!UICONTROL Custom Code]** per il tipo di elemento dati. Da qui, seleziona **[!UICONTROL Apri editor]** nel pannello di destra.

![Seleziona tipo di elemento dati](../../../images/extensions/client/privacy/data-element-type.png)

Nella finestra di dialogo visualizzata, definisci una funzione JavaScript che gestirà le identità recuperate. Il callback deve accettare un singolo argomento di tipo oggetto (`ids` nell&#39;esempio seguente). La funzione può quindi gestire gli ID in base alle tue preferenze e richiamare eventuali variabili e funzioni globalmente disponibili sul sito per ulteriori elaborazioni.

>[!NOTE]
>
>Per ulteriori informazioni sulla struttura dell&#39;oggetto `ids` che la funzione di callback deve gestire, fare riferimento agli [esempi di codice](../../../../privacy-service/js-library.md#samples) forniti nella panoramica della libreria JavaScript per la privacy.

Al termine, selezionare **[!UICONTROL Salva]**.

![Definisci funzione di callback](../../../images/extensions/client/privacy/define-custom-code.png)

Puoi continuare a creare altri elementi dati con codice personalizzato se richiedi callback diversi per eventi diversi.

### Creare una regola con un’azione sulla privacy

Dopo aver configurato un elemento dati di callback per gestire gli ID recuperati, puoi creare una regola che richiama l&#39;estensione Adobe Privacy ogni volta che si verifica un determinato evento sul sito insieme a qualsiasi altra condizione richiesta.

Durante la configurazione dell&#39;azione per la regola, seleziona **[!UICONTROL Adobe Privacy]** per l&#39;estensione. Per il tipo di azione, selezionare una delle [tre funzioni](#using) fornite dall&#39;estensione.

![Seleziona tipo di azione](../../../images/extensions/client/privacy/action-type.png)

Il pannello di destra richiede di selezionare un elemento dati che fungerà da callback dell’azione. Selezionare l&#39;icona del database (![Icona database](/help/images/icons/database.png)) e scegliere dall&#39;elenco l&#39;elemento dati creato in precedenza. Seleziona **[!UICONTROL Mantieni modifiche]** per continuare.

![Seleziona elemento dati](../../../images/extensions/client/privacy/add-data-element.png)

Da qui puoi continuare a configurare la regola in modo che l’azione Privacy dell’Adobe venga attivata in base agli eventi e alle condizioni richieste. Al termine, selezionare **[!UICONTROL Salva]**.

![Salva la regola](../../../images/extensions/client/privacy/save-rule.png)

Ora puoi aggiungere la regola a una libreria da distribuire come build sul sito web per il test. Per ulteriori informazioni, consulta la panoramica sul flusso di pubblicazione dei [tag](../../../ui/publishing/overview.md).

## Disattivare o disinstallare l’estensione

Dopo aver installato l&#39;estensione, puoi disabilitarla o eliminarla. Fai clic su **[!UICONTROL Configura]** nella scheda Adobe Privacy nelle estensioni installate, quindi seleziona **[!UICONTROL Disabilita]** o **[!UICONTROL Disinstalla]**.

## Passaggi successivi

Questa guida descrive l’utilizzo dell’estensione tag Adobe Privacy nell’interfaccia utente. Per ulteriori informazioni sulle funzionalità fornite dall&#39;estensione, inclusi esempi di utilizzo con codice non elaborato, vedi la [Panoramica sulla libreria JavaScript Privacy](../../../../privacy-service/js-library.md) nella documentazione di Privacy Service.
