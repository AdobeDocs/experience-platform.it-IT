---
title: Pacchetti di estensione privati condivisi
description: Scopri come condividere i pacchetti di estensione privati nei tag Adobe Experience Platform.
source-git-commit: f45f58b4679b619708204cdb0c18174a4836ce8d
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Pacchetti di estensione privati condivisi

I tag Adobe Experience Platform ora supportano **[!UICONTROL Autorizzazioni di utilizzo]**, una potente funzione che consente di condividere in modo sicuro i pacchetti di estensione privati con partner attendibili senza renderli disponibili al pubblico nel catalogo delle estensioni. Questa funzione crea un ponte sicuro tra le organizzazioni, consentendoti di sfruttare il codice di estensione personalizzato dell’altra organizzazione mantenendo al contempo la privacy e il controllo sulle soluzioni proprietarie.

## Condivisione di pacchetti di estensione con altre organizzazioni

>[!NOTE]
>
>I pacchetti di estensione devono avere una versione privata o pubblica per essere condivisi tramite [!UICONTROL Autorizzazioni di utilizzo]. Le versioni contrassegnate come Disponibilità di sviluppo non sono idonee per la condivisione e non verranno visualizzate nel menu a discesa Autorizzazione. Ciò si applica anche se è già stata condivisa una versione precedente (ad esempio, 1.0.0). Le versioni più recenti (ad esempio, 1.0.1) devono essere rese almeno private prima di poter essere autorizzate o installate dalle organizzazioni riceventi.
>
>Tutte le indicazioni relative alla condivisione di pacchetti di estensione privati si applicano anche se successivamente scegli di renderli pubblici. Le stesse considerazioni su visibilità, controllo delle versioni, sicurezza, compatibilità, supporto e documentazione rimangono rilevanti indipendentemente dallo stato di disponibilità del pacchetto.

I pacchetti di estensione pubblici e privati possono essere condivisi tramite [!UICONTROL Autorizzazioni di utilizzo], anche se le estensioni nella disponibilità Sviluppo non possono avere autorizzazioni associate a essi.

Le organizzazioni spesso sviluppano estensioni specializzate personalizzate in base ai propri requisiti aziendali specifici. Queste estensioni possono contenere logica proprietaria, integrazioni personalizzate o configurazioni sensibili che non devono essere rese pubbliche. Le autorizzazioni di utilizzo risolvono questo problema consentendo:

- **Condivisione selettiva**: condividere estensioni private solo con organizzazioni partner attendibili
- **Privacy mantenuta**: escludi dal catalogo pubblico il codice di estensione sensibile
- **Sviluppo collaborativo**: consente ai partner attendibili di beneficiare delle soluzioni personalizzate
- **Accesso controllato**: mantieni il controllo completo su chi può accedere e utilizzare le estensioni private

Il processo di condivisione coinvolge due partecipanti chiave:

1. **Organizzazione di condivisione**: l&#39;organizzazione proprietaria e condivisa del pacchetto di estensione privato
2. **Organizzazione di ricezione**: l&#39;organizzazione attendibile che ottiene l&#39;accesso all&#39;estensione condivisa

Quando viene condivisa una versione privata, l’organizzazione ricevente ottiene l’accesso a tale versione specifica, creando una connessione diretta tra le due organizzazioni. Se una versione più recente viene successivamente resa privata, sarà disponibile anche per l’organizzazione ricevente senza richiedere alcun passaggio aggiuntivo da parte loro.

## Creare un’autorizzazione per l’utilizzo del pacchetto di estensione

Per condividere un&#39;estensione, accedi all&#39;interfaccia utente di Data Collection e seleziona **[!UICONTROL Tag]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà esistente o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nell&#39;area di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Autorizzazioni di utilizzo]**.

In questo caso, viene visualizzato un elenco delle autorizzazioni condivise esistenti organizzate in due categorie:

- **Condiviso con questa organizzazione**: estensioni condivise con te da altre organizzazioni.
- **Condiviso con altre organizzazioni**: estensioni condivise con altre organizzazioni.

Selezionare **[!UICONTROL Aggiungi autorizzazione]**.

![La scheda [!UICONTROL Autorizzazioni di utilizzo] mostra un elenco di estensioni condivise con questa organizzazione, evidenziando [!UICONTROL Aggiungi autorizzazione]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>È necessario ottenere **`Organization ID`** dell&#39;organizzazione di destinazione come proprietario dell&#39;organizzazione. Non è possibile eseguire ricerche per nome nelle organizzazioni.

Seleziona l&#39;**[!UICONTROL Estensione]** che desideri condividere dalle estensioni disponibili nel menu a discesa. L’elenco mostra le estensioni di proprietà dell’organizzazione e il loro stato di disponibilità. Le estensioni la cui versione più recente è disponibile in **Sviluppo** non verranno visualizzate in questo elenco.

Quindi, immetti l&#39;ID dell&#39;organizzazione ricevente, quindi seleziona **[!UICONTROL Salva]**.

![Nella pagina [!UICONTROL Crea autorizzazione per l&#39;utilizzo del pacchetto di estensione] sono visualizzati l&#39;estensione selezionata e l&#39;ID organizzazione Adobe immesso, con l&#39;evidenziazione di [!UICONTROL Salva]](../images/shared-extensions/save-authorization.png)

Sei tornato alla scheda [!UICONTROL Autorizzazioni di utilizzo] in cui puoi visualizzare l&#39;estensione nell&#39;elenco **[!UICONTROL Condiviso con altre organizzazioni]**. Lo stato visualizzato **In attesa di approvazione** fino a quando l&#39;organizzazione ricevente non approva l&#39;autorizzazione, nel qual caso verrà aggiornato a **Approvato**.

![La scheda [!UICONTROL Autorizzazioni di utilizzo] mostra un elenco di estensioni condivise con altre organizzazioni, evidenziando la nuova autorizzazione](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>Puoi anche condividere le estensioni direttamente dal **[!UICONTROL Catalogo estensioni]** selezionando il menu (⋯) nella scheda delle estensioni, quindi seleziona l&#39;opzione di condivisione dal menu.

Quando un&#39;autorizzazione è attiva, l&#39;estensione condivisa visualizza un contrassegno ***Condivisione*** nel catalogo che indica che è condivisa con altre organizzazioni.

![La scheda [!UICONTROL Catalogo] che mostra l&#39;estensione condivisa con il badge](../images/shared-extensions/sharing-badge.png)

## Autorizzare e gestire le estensioni condivise

>[!NOTE]
>
>In qualità di organizzazione ricevente, puoi approvare o rifiutare solo le estensioni condivise. Non è possibile gestire o modificare i dettagli dell’autorizzazione, in quanto sono controllati dall’organizzazione che condivide.

Per autorizzare un&#39;estensione condivisa per la tua organizzazione, passa all&#39;interfaccia utente di Data Collection e seleziona **[!UICONTROL Tag]** dalla navigazione a sinistra, quindi seleziona la proprietà. Quindi, seleziona **[!UICONTROL Estensioni]** nell&#39;area di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Autorizzazioni di utilizzo]**.

Puoi visualizzare un elenco di estensioni condivise, comprese quelle **In attesa di approvazione** nella sezione **[!UICONTROL Condivise con questa organizzazione]**. Seleziona l&#39;estensione da approvare, quindi fai clic su **[!UICONTROL Approva]**.

![La scheda [!UICONTROL Autorizzazioni di utilizzo] mostra un elenco di estensioni condivise con questa organizzazione con l&#39;estensione in attesa di approvazione selezionata, evidenziando [!UICONTROL Approva]](../images/shared-extensions/approve-authorization.png)

>[!NOTE]
>
>Puoi anche rifiutare una richiesta nella scheda **[!UICONTROL Autorizzazioni di utilizzo]** se l&#39;estensione condivisa non è più richiesta dalla tua organizzazione.

Seleziona **[!UICONTROL OK]** nella finestra di dialogo **[!UICONTROL Utilizzi di autorizzazione]**.

![Finestra di dialogo [!UICONTROL Utilizzo autorizzazioni], con evidenziazione di [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

Sei tornato alla scheda [!UICONTROL Autorizzazioni di utilizzo] in cui puoi vedere che l&#39;estensione ora mostra uno stato **Approvato**.

![La scheda [!UICONTROL Autorizzazioni di utilizzo] mostra un elenco di estensioni condivise con questa organizzazione, evidenziando l&#39;estensione con lo stato Approvato](../images/shared-extensions/approved-authorization.png)

Una volta approvata l’autorizzazione, l’estensione è disponibile nel catalogo e può essere installata e utilizzata come qualsiasi altra estensione. L&#39;estensione condivisa visualizza un contrassegno ***Ricezione*** che indica che si tratta di un&#39;estensione condivisa con te da un&#39;altra organizzazione.

![La scheda [!UICONTROL Catalogo] che mostra l&#39;estensione condivisa con il badge &quot;Ricezione&quot;](../images/shared-extensions/receiving-badge.png)

## Revoca delle autorizzazioni

In qualità di organizzazione proprietaria, è possibile eliminare un’autorizzazione in qualsiasi momento, indipendentemente dal suo stato corrente (In attesa di approvazione, Rifiutata o Approvata).

**Se l&#39;estensione non è mai stata resa pubblica:**
- Qualsiasi versione privata già installata dall’organizzazione ricevente continuerà a essere visualizzata nell’elenco delle estensioni installate.
- Se l’organizzazione ricevente non ha mai installato l’estensione, questa non verrà più visualizzata in nessuna parte dell’interfaccia.

**Se l&#39;estensione è stata resa pubblica:**
- Tutte le versioni private installate dall’organizzazione ricevente rimangono visibili nell’elenco delle estensioni installate.
- Se non hanno mai installato la tua versione privata, vedranno comunque l’ultima versione pubblica nel loro catalogo e potranno installarla.
- Puoi anche effettuare il downgrade dalla versione privata alla versione pubblica più recente, se lo desideri.

Quando revochi un’autorizzazione, l’organizzazione ricevente mantiene alcuni diritti per proteggere le implementazioni esistenti:

- **Utilizzo continuato**: l&#39;organizzazione ricevente può continuare a utilizzare qualsiasi versione privata già installata, anche dopo la revoca dell&#39;accesso.
- **Protezione compilazione**: se l&#39;organizzazione ricevente ha installato la versione privata 1.0.0 e successivamente si rilascia la versione privata 1.0.1, non vedrà la versione più recente ma potrà continuare a generare la versione 1.0.0 senza interruzioni.
- **Aggiornamenti futuri**: se successivamente rendi pubblica l&#39;estensione (ad esempio, rilasciando pubblicamente la versione 2.0.0), l&#39;organizzazione ricevente può eseguire l&#39;aggiornamento dalla versione privata 1.0.0 direttamente alla nuova versione pubblica 2.0.0.

>[!IMPORTANT]
>
>La revoca dell’autorizzazione non interrompe le build o le implementazioni esistenti. Le organizzazioni riceventi mantengono l&#39;accesso a tutte le versioni private già installate per garantire la Business Continuity.

## Passaggi successivi

Questo documento illustra come utilizzare la funzione di estensione condivisa in Experience Platform. Per informazioni sullo sviluppo di estensioni, consulta la [guida utente per lo sviluppo di estensioni](./getting-started.md).

Per una panoramica di alto livello sullo sviluppo delle estensioni in Experience Platform, consulta la [documentazione sulla panoramica](./overview.md).
