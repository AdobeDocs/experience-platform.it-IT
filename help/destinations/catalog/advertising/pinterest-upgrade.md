---
title: Migrazione della destinazione pinterest alla nuova API. Azione del cliente richiesta.
description: Pinterest sta rendendo obsoleta l’API dell’inserzionista v4 attualmente utilizzata dalla destinazione Pinterest in Real-Time CDP. Comprendi le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Aggiornamento della destinazione pinterest alla nuova API. Azione cliente richiesta entro il 15 dicembre 2023

## Cosa succede?

Pinterest sta rendendo obsoleta l’API dell’inserzionista v4 attualmente utilizzata da [Destinazione pinterest](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP. Adobe sta lavorando con Pinterest e sta aggiornando la destinazione per utilizzare [API inserzionista v5](https://developers.pinterest.com/docs/getting-started/migration/). Leggi questa pagina per comprendere le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.

## Perché mi viene inviata una notifica?

Abbiamo identificato la tua organizzazione come dotata di flussi di dati attivi per attivare i tipi di pubblico in Pinterest.

## Qual è il piano?

Adobe sta rilasciando una nuova scheda di destinazione Pinterest che sfrutta l’API Pinterest v5 e manterrà i flussi di dati esistenti nella nuova connessione.

## Devo fare qualcosa per mantenere attivi i tipi di pubblico?

Sì, una volta completato l’aggiornamento di Adobe (previsto per il 16 novembre), dovrai ripetere l’autenticazione in Pinterest con l’account dell’inserzionista Pinterest in Adobe Experience Platform. Consulta le istruzioni dettagliate di seguito.

### Autentica di nuovo in Pinterest {#reauthenticate}

1. Vai a **[!UICONTROL Destinazioni > Account]** e utilizza il filtro sullo schermo per filtrare solo la destinazione Pinterest.
   ![Filtra solo account Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Il giorno **(Nuovo) Pinterest** destinazione, selezionare il simbolo dei tre punti ... e selezionare **[!UICONTROL Modifica dettagli]**.
   ![Seleziona Modifica dettagli](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Seleziona **[!UICONTROL Riconnetti OAuth]** e accedi al tuo account Pinterest.
   ![Seleziona Riconnetti OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Adobe di notifica della nuova autenticazione per **[!UICONTROL (Nuovo) Pinterest]** destinazione.

### Disabilita i flussi esistenti nella vecchia destinazione e abilita i flussi nella nuova destinazione {#disable-old-enable-new-flows}

Quindi, devi disattivare manualmente i flussi esistenti per la vecchia scheda e abilitare i flussi per la nuova scheda.

>[!IMPORTANT]
>
>Dopo la nuova autenticazione, puoi contattare Adobe ed eseguiremo questo secondo passaggio per te. Se preferisci eseguire questo passaggio manualmente, segui i passaggi seguenti:

1. Vai a **[!UICONTROL Destinazioni > Sfoglia]** e utilizza il filtro sullo schermo per filtrare **[!UICONTROL (Nuovo) Pinterest]** e **[!UICONTROL (Obsoleto) Pinterest]** solo destinazioni.
   ![Filtrare i flussi di dati di Pinterest solo nella scheda Sfoglia](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Seleziona il nome della connessione con collegamento ipertestuale (campagna fedeltà nell’esempio della schermata precedente) e cambia il **[!UICONTROL Abilita]** passa a **disattivato** per la connessione precedente e per **il** per la nuova connessione.
   ![Attiva per le nuove connessioni e disattiva per le connessioni precedenti](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. Confronta l’elenco dei tipi di pubblico attivati nel flusso di dati precedente e nuovo e assicurati di non avere nuovi tipi di pubblico nei flussi precedenti che mancano nei nuovi flussi.

Anche se non sono previste interruzioni delle campagne, ricorda di verificare nell’interfaccia utente di Pinterest che tutto funzioni come previsto.

## Puoi condividere alcune timeline di alto livello?

Sì, consulta:

**Entro il 16 novembre**: la nuova destinazione è pronta e dovresti vedere due schede Pinterest una accanto all’altra nel catalogo; tutti i flussi di dati esistenti sulla scheda Pinterest corrente vengono copiati nella nuova destinazione.

![affiancata la vecchia e la nuova destinazione Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Dopo il 16 novembre, la destinazione Pinterest legacy è contrassegnata **[!UICONTROL Obsoleto]**. <span class="preview">Eventuali modifiche apportate ai flussi di dati della destinazione Pinterest (obsoleta) dopo il 16 novembre *non* vengono automaticamente trasferite alla nuova destinazione Pinterest. </span>
>Ad esempio, *non consigliare* che attivi nuovi tipi di pubblico nella vecchia destinazione dopo il 16 novembre. In tal caso, dovrà seguire la [passaggi di attivazione regolari](/help/destinations/ui/activate-segment-streaming-destinations.md) per aggiungere il pubblico alla nuova destinazione una volta intraprese le azioni del cliente.

**Entro il 15 dicembre**: <span class="preview">Azione del cliente</span>. È necessario ripetere l&#39;autenticazione in Pinterest in modo che la nuova scheda sia collegata a Pinterest (istruzioni più avanti). Una volta fatto questo, contattaci.

I flussi di dati a Pinterest nella vecchia scheda devono essere disabilitati e quelli nella nuova scheda devono essere abilitati. Puoi farlo manualmente nell’interfaccia utente, oppure rivolgiti a Adobe e noi lo faremo per te.

## Altri elementi da annotare

Dopo aver abilitato i flussi di dati sulla nuova scheda di destinazione e aver disabilitato i flussi di dati sulle vecchie schede di destinazione, dovresti vedere nessuna interruzione nelle campagne o nel numero di profili qualificati nei tipi di pubblico provenienti da Adobe Real-Time CDP.
