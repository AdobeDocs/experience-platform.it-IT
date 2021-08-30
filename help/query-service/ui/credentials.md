---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;editor query;editor query;editor query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio query
topic-legacy: guide
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: aabe89f236bc68a51f14ee1909687982f4fe5973
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Guida alle credenziali

Adobe Experience Platform Query Service consente di connettersi con client esterni. È possibile connettersi a questi client esterni utilizzando credenziali in scadenza o credenziali in scadenza.

## Credenziali in scadenza

È possibile utilizzare le credenziali in scadenza per configurare rapidamente una connessione a un client esterno.

![](../images/ui/credentials/expiring-credentials.png)

La sezione **[!UICONTROL Credenziali in scadenza]** fornisce le seguenti informazioni:

- **[!UICONTROL Host]**: Nome dell&#39;host a cui ti connetterai. Per la connessione al servizio query, verrà incluso il nome dell’organizzazione IMS attualmente in uso.
- **[!UICONTROL Porta]**: Numero di porta dell&#39;host a cui ci si connette.
- **[!UICONTROL Database]**: Nome del database a cui ci si connette.
- **[!UICONTROL Nome utente]**: Nome utente che verrà utilizzato per connettersi al servizio query.
- **[!UICONTROL Password]**: Password da utilizzare per la connessione al servizio query.
- **[!UICONTROL Comando]** PSQL: Comando che ha inserito automaticamente tutte le informazioni pertinenti per la connessione a Query Service tramite PSQL nella riga di comando.
- **[!UICONTROL Scade]**: Data di scadenza delle credenziali in scadenza. Le credenziali scadono 24 ore dopo la generazione.

## Credenziali non in scadenza

È possibile utilizzare le credenziali non in scadenza per impostare una connessione più permanente a un client esterno.

Per creare un set di credenziali non in scadenza, selezionare **[!UICONTROL Genera credenziali]**.

>[!NOTE]
>
>Prima di poter creare credenziali non in scadenza, è necessario disporre delle autorizzazioni **Sandbox** e **Gestisci integrazione servizio query**. Per informazioni su come assegnare queste autorizzazioni, leggi la documentazione su [Controllo accessi](../../access-control/home.md).

![](../images/ui/credentials/generate-credentials.png)

Viene visualizzata la finestra modale per la generazione delle credenziali. Per creare credenziali non in scadenza, è necessario fornire i seguenti dettagli:

- **[!UICONTROL Nome]**: Nome delle credenziali che si sta generando.
- **[!UICONTROL Descrizione]**: (Facoltativo) Una descrizione delle credenziali che stai generando.
- **[!UICONTROL Assegnato a]**: Utente a cui verranno assegnate le credenziali. Questo valore deve essere l&#39;indirizzo e-mail dell&#39;utente che sta creando le credenziali.
- **[!UICONTROL Password]**  (opzionale) Una password opzionale per le tue credenziali. Se la password non è impostata, Adobe genererà automaticamente una password.

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Genera credenziali]** per generare le credenziali.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Una volta selezionato il pulsante **[!UICONTROL Genera credenziali]**, un file di configurazione che contiene informazioni quali il nome dell&#39;account tecnico, l&#39;ID dell&#39;account tecnico e le credenziali. Poiché in Adobe **non** viene registrata la credenziale generata, **è necessario** memorizzare in modo sicuro il file scaricato e conservare un record della credenziale.
>
>Inoltre, se le credenziali non vengono utilizzate per 90 giorni, verranno eliminate.

Dopo aver salvato le credenziali generate, seleziona **[!UICONTROL Chiudi]**. È ora possibile visualizzare un elenco di tutte le credenziali non in scadenza.

![](../images/ui/credentials/list-credentials.png)

È possibile modificare o eliminare le credenziali non in scadenza. Per modificare una credenziale non in scadenza, seleziona l’icona a forma di matita (![](../images/ui/credentials/edit-icon.png)). Per eliminare una credenziale non in scadenza, seleziona l’icona Elimina (![](../images/ui/credentials/delete-icon.png)).

Quando si modifica una credenziale non in scadenza, viene visualizzato un modale. Puoi fornire i seguenti dettagli da aggiornare:

- **[!UICONTROL Nome]**: Nome delle credenziali che si sta generando.
- **[!UICONTROL Descrizione]**: (Facoltativo) Una descrizione delle credenziali che stai generando.
- **[!UICONTROL Assegnato a]**: Utente a cui verranno assegnate le credenziali. Questo valore deve essere l&#39;indirizzo e-mail dell&#39;utente che sta creando le credenziali.

![](../images/ui/credentials/update-credentials.png)

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Aggiorna account]** per completare l&#39;aggiornamento delle tue credenziali.

## Utilizzo delle credenziali per la connessione a client esterni

È possibile utilizzare le credenziali in scadenza o non in scadenza per connettersi con client esterni, ad esempio Aqua Data Studio, Looker o Power BI.

Quando ti connetti a questi client esterni, in genere devi includere le seguenti informazioni:

- **Server/Host**: Il nome del server/host a cui ti connetti. Questo valore si presenta sotto forma di `server.adobe.io` e si trova sotto **[!UICONTROL Host]** nella sezione delle credenziali in scadenza.
- **Porta**: La porta del server/host a cui ti stai connettendo. Questo valore si trova in **[!UICONTROL Porta]** nella sezione delle credenziali in scadenza. Un valore di esempio per la porta è `80`.
- **Nome utente**: Nome utente per l’utente che si connette al client esterno. Questo si presenta sotto forma di `ID@AdobeOrg` e si trova sotto **[!UICONTROL Nome utente]** nella sezione delle credenziali in scadenza.
- **Password**: Password per l&#39;utente che si connette al client esterno. Se utilizzi credenziali in scadenza, puoi trovarlo in **[!UICONTROL Password]** nella sezione relativa alle credenziali in scadenza. Se utilizzi credenziali non in scadenza, questo valore è composto sia dall’ID account tecnico che dalla credenziale nel modulo: `technicalAccountId:credential`.
- **Database**: Database a cui ci si connette. Questo valore si trova in **[!UICONTROL Database]** nella sezione delle credenziali in scadenza. Un valore di esempio per il database è `prod:all`.

## Passaggi successivi

Ora che si capisce come funzionano sia le credenziali in scadenza che quelle in scadenza, è possibile utilizzare queste credenziali per connettersi a client esterni. Per ulteriori informazioni dettagliate sui client esterni, leggere la [guida alla connessione dei client a Query Service](../clients/overview.md).