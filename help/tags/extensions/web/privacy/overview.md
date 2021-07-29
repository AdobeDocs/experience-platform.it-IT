---
title: Panoramica dell’estensione Adobe Privacy
description: Scopri l’estensione Adobe Privacy tag in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 92%

---

# Panoramica dell’estensione Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L&#39;estensione Adobe Privacy fornisce funzionalità per la raccolta e la rimozione degli ID utente assegnati agli utenti finali dalle soluzioni Adobe.

## Configura le soluzioni durante l&#39;installazione

Quando installi l&#39;estensione Adobe Privacy dal catalogo delle estensioni, ti viene richiesto di selezionare le soluzioni che desideri aggiornare. Al momento puoi aggiornare le soluzioni seguenti:

* Analytics (AA)
* Audience Manager (AAM)
* Target
* Visitor Service
* AdCloud
* Seleziona una o più soluzioni, quindi fai clic su Update.
* Dopo aver selezionato e configurato le soluzioni, fai clic su Salva. L&#39;estensione Adobe Privacy viene aggiunta all&#39;elenco delle estensioni installate.

   Le opzioni di ciascuna soluzione sono descritte di seguito.

### Analytics

![](../../../images/ext-privacy-aa.jpg)

Per impostazione predefinita, devi fornire la suite di rapporti immettendo una stringa o selezionando un elemento di dati.

Per configurare altri elementi, fai clic su **[!UICONTROL Scegli un elemento]**, seleziona l’elemento da configurare, quindi fai clic su **[!UICONTROL Aggiungi]** e immetti il parametro richiesto o un elemento dati.

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

Fai clic su **[!UICONTROL Scegli un elemento]**, seleziona l’elemento che desideri configurare, quindi fai clic su **[!UICONTROL Aggiungi]** e inserisci il parametro richiesto o un elemento dati. Al momento, è possibile configurare solo `aamUUIDCookieName`.

### Target

![](../../../images/ext-privacy-target.jpg)

Immetti il codice client Target.

### Servizio visitatori

![](../../../images/ext-privacy-visitor.jpg)

Immetti il tuo IMS Organization ID.

### AdCloud

![](../../../images/ext-privacy-adcloud.jpg)

Non esistono parametri specifici da configurare per AdCloud.

## Configura l&#39;estensione Adobe Privacy

Dopo aver installato l&#39;estensione, puoi disabilitarla o eliminarla. Fai clic su **[!UICONTROL Configura]** nella scheda Adobe Privacy nelle estensioni installate, quindi seleziona **[!UICONTROL Disabilita]** o **[!UICONTROL Disinstalla]**.

## Azioni

Le azioni seguenti sono disponibili quando configuri una regola utilizzando l&#39;estensione Adobe Privacy.

### Recupera identità

Quando l&#39;evento e le condizioni vengono soddisfatte, recupera le informazioni di identità memorizzate per il visitatore.

Immetti il nome di una funzione JavaScript a cui desideri trasmettere i dati. Questa funzione o metodo gestisce le identità recuperate. Puoi decidere di memorizzarle, visualizzarle o inviarle all&#39;API Adobe RGPD.

### Rimuovi le identità

Quando l&#39;evento e le condizioni vengono soddisfatte, rimuovi le informazioni di identità memorizzate per il visitatore.

Immetti il nome di una funzione JavaScript a cui desideri trasmettere i dati. Questa funzione o metodo gestisce le identità recuperate. Puoi decidere di memorizzarle, visualizzarle o inviarle all&#39;API Adobe RGPD.

### Recupera ed elimina le identità

Quando l&#39;evento e le condizioni vengono soddisfatte, recupera le informazioni di identità memorizzate per il visitatore, quindi rimuovile.

## Esercitazione: configurazione dell’estensione Privacy

Di seguito è riportato un esempio su come impostare un elemento dati e utilizzarlo con l’estensione Privacy.

1. Crea un elemento dati denominato `privacyFunc`.

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. Crea una regola da eseguire al caricamento della libreria (inizio pagina), con un&#39;azione dell&#39;estensione Adobe Privacy. Seleziona `privacyFunc` come elemento dati.

   * **Estensione:** Adobe Privacy
   * **Tipo azione:** Recupera identità
Questo tipo di azione visualizza le identità create, rimosse o non rimosse.
   * **Nome:** Recupera identità

1. Aggiorna la libreria di sviluppo, quindi pubblica ed esegui il test.
