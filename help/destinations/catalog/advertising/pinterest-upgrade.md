---
title: Migrazione della destinazione pinterest alla nuova API. Azione del cliente richiesta.
description: Pinterest sta rendendo obsoleta l’API dell’inserzionista v4 attualmente utilizzata dalla destinazione Pinterest in Real-Time CDP. Comprendi le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.
hide: true
hidefromtoc: true
source-git-commit: dbbdb62c996466499b70990decba58ecaf1be901
workflow-type: tm+mt
source-wordcount: '711'
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

Sì, una volta che Adobe completa l’aggiornamento e rilascia la nuova destinazione Pinterest, è necessario autenticare nuovamente in Pinterest con l’account dell’inserzionista Pinterest in Real-Time CDP. Consulta le istruzioni dettagliate di seguito.

### Autentica di nuovo in Pinterest {#reauthenticate}

1. Vai a **[!UICONTROL Destinazioni > Account]** e utilizza il filtro sullo schermo per filtrare solo la destinazione Pinterest.
   ![Filtra solo account Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Il giorno **(Nuovo) Pinterest** destinazione, selezionare il simbolo dei tre punti ... e selezionare **[!UICONTROL Modifica dettagli]**.
   ![Seleziona Modifica dettagli](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Seleziona **[!UICONTROL Riconnetti OAuth]** e accedi al tuo account Pinterest.
   ![Seleziona Riconnetti OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Passa all’azione nella sezione seguente

### Disabilita i flussi esistenti nella vecchia destinazione e abilita i flussi nella nuova destinazione {#disable-old-enable-new-flows}

Quindi, devi disabilitare manualmente i flussi esistenti per la vecchia scheda di destinazione **[!UICONTROL (Obsoleto) Pinterest]** e abilita i flussi verso la nuova scheda **[!UICONTROL (Nuovo) Pinterest]**.

1. Vai a **[!UICONTROL Destinazioni > Sfoglia]** e utilizza il filtro sullo schermo per filtrare **[!UICONTROL (Nuovo) Pinterest]** e **[!UICONTROL (Obsoleto) Pinterest]** solo destinazioni.
   ![Filtrare i flussi di dati di Pinterest solo nella scheda Sfoglia](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Seleziona il nome della connessione ipertestuale (campagna fedeltà nell’esempio della schermata precedente) al **[!UICONTROL (Obsoleto) Pinterest]** destinazione e cambiare il **[!UICONTROL Abilita]** passa a **disattivato**.
   ![Attiva per le nuove connessioni e disattiva per le connessioni precedenti](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-old-destination.png)
3. Seleziona il nome della connessione ipertestuale (campagna fedeltà nell’esempio della schermata precedente) al **[!UICONTROL (Nuovo) Pinterest]** destinazione e cambiare il **[!UICONTROL Abilita]** passa a **il**.
   ![Attiva per le nuove connessioni e disattiva per le connessioni precedenti](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)
4. Confronta l’elenco dei tipi di pubblico attivati nel flusso di dati precedente e nuovo e assicurati di non avere nuovi tipi di pubblico nei flussi precedenti che mancano nei nuovi flussi.

Anche se non sono previste interruzioni delle campagne, ricorda di verificare nell’interfaccia utente di Pinterest che tutto funzioni come previsto.

## Puoi condividere alcune timeline di alto livello?

Sì, consulta:

**Entro il 16 novembre 2023**: la nuova destinazione è pronta e dovresti vedere due schede Pinterest una accanto all’altra nel catalogo; tutti i flussi di dati esistenti sulla scheda Pinterest corrente vengono copiati nella nuova destinazione.

![affiancata la vecchia e la nuova destinazione Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Dopo il 16 novembre 2023, la destinazione Pinterest legacy è contrassegnata **[!UICONTROL Obsoleto]**. <span class="preview">Eventuali modifiche apportate ai flussi di dati della destinazione Pinterest (obsoleta) dopo il 16 novembre *non* vengono automaticamente trasferite alla nuova destinazione Pinterest. </span>
>Ad esempio, *non consigliare* che attivi nuovi tipi di pubblico nella vecchia destinazione dopo il 16 novembre. In tal caso, dovrà seguire la [passaggi di attivazione regolari](/help/destinations/ui/activate-segment-streaming-destinations.md) per aggiungere il pubblico alla nuova destinazione una volta intraprese le azioni del cliente.

**Entro il 15 dicembre 2023**: <span class="preview">Azione cliente 1</span>. È necessario eseguire nuovamente l&#39;autenticazione in Pinterest in modo che la nuova scheda sia collegata a Pinterest. Visualizzare le istruzioni complete in [questa sezione](#reauthenticate).

<span class="preview">Azione cliente 2</span>Quindi devi disattivare i flussi di dati verso Pinterest nella vecchia scheda e abilitare i flussi di dati nella nuova scheda. Visualizzare le istruzioni complete in [questa sezione](#disable-old-enable-new-flows).

>[!IMPORTANT]
>
>Dopo il 15 dicembre 2023, Adobe non garantisce l’integrità dei flussi di dati verso il vecchio **[!UICONTROL (Obsoleto) Pinterest]** destinazione.

## Altri elementi da annotare

Dopo aver abilitato i flussi di dati sulla nuova scheda di destinazione e aver disabilitato i flussi di dati sulle vecchie schede di destinazione, dovresti vedere nessuna interruzione nelle campagne o nel numero di profili qualificati nei tipi di pubblico provenienti da Adobe Real-Time CDP.
