---
title: Migrazione della destinazione pinterest alla nuova API. Azione del cliente richiesta.
description: Pinterest sta rendendo obsoleta l’API dell’inserzionista v4 attualmente utilizzata dalla destinazione Pinterest in Real-Time CDP. Comprendi le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: 3968c8e2a0ebd2084a7047fb41e2b85c5da7a6e7
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Aggiornamento della destinazione pinterest alla nuova API. Azione cliente richiesta entro il 18 gennaio 2024.

>[!IMPORTANT]
>
>Gli elementi azione cliente in questa pagina sono applicabili se l’organizzazione ha impostato flussi di dati per esportare dati in Pinterest prima del 16 novembre 2023, data in cui il nuovo **[!UICONTROL Pinterest]** La destinazione, utilizzando l’API Pinterest più recente, è stata aggiunta al catalogo delle destinazioni.

## Cosa succede?

Pinterest ha dichiarato obsoleta l&#39;API dell&#39;inserzionista v4 utilizzata da [Destinazione pinterest](/help/destinations/catalog/advertising/pinterest.md) in Real-Time CDP. Adobe: la destinazione è stata aggiornata per utilizzare [API inserzionista v5](https://developers.pinterest.com/docs/getting-started/migration/). Leggi questa pagina per comprendere le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.

## Perché mi viene inviata una notifica?

Abbiamo identificato la tua organizzazione come dotata di flussi di dati attivi per attivare i tipi di pubblico in Pinterest.

## Qual è il piano?

Adobe sta rilasciando una nuova scheda di destinazione Pinterest che sfrutta l’API Pinterest v5 e manterrà i flussi di dati esistenti nella nuova connessione.

## Devo fare qualcosa per mantenere attivi i tipi di pubblico?

Sì, prima del 18 gennaio 2024, è necessario eseguire l’autenticazione nella nuova destinazione Pinterest con l’account dell’inserzionista Pinterest in Real-Time CDP. Consulta le istruzioni dettagliate di seguito.

### Autentica di nuovo in Pinterest {#reauthenticate}

1. Vai a **[!UICONTROL Destinazioni > Account]** e utilizza il filtro sullo schermo per filtrare solo la destinazione Pinterest.
   ![Filtra solo account Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Il giorno **Pinterest** destinazione, selezionare il simbolo dei tre punti ... e selezionare **[!UICONTROL Modifica dettagli]**.
   ![Seleziona Modifica dettagli](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Seleziona **[!UICONTROL Riconnetti OAuth]** e accedi al tuo account Pinterest.
   ![Seleziona Riconnetti OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Passa all’azione nella sezione seguente

### Abilita i flussi nella nuova destinazione {#disable-old-enable-new-flows}

Quindi, devi abilitare i flussi di dati alla nuova scheda **[!UICONTROL (Nuovo) Pinterest]**.

1. Vai a **[!UICONTROL Destinazioni > Sfoglia]** e utilizza il filtro sullo schermo per filtrare **[!UICONTROL Pinterest]** solo destinazione.
   ![Filtrare i flussi di dati di Pinterest solo nella scheda Sfoglia](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Seleziona il nome della connessione ipertestuale (campagna fedeltà nell’esempio della schermata precedente) al **[!UICONTROL Pinterest]** destinazione e cambiare il **[!UICONTROL Abilita]** passa a **il**.
   ![Attiva per le nuove connessioni e disattiva per le connessioni precedenti](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Puoi condividere alcune timeline di alto livello?

Sì, consulta:

**Entro il 16 novembre 2023**: la nuova destinazione è pronta e dovresti vedere due schede Pinterest una accanto all’altra nel catalogo fino a quando Pinterest non smette di supportare la vecchia API v4. Tutti i flussi di dati esistenti nella scheda Pinterest corrente vengono copiati nella nuova destinazione.

![affiancata la vecchia e la nuova destinazione Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Dopo il 16 novembre 2023, la destinazione Pinterest legacy è contrassegnata **[!UICONTROL Obsoleto]**. <span class="preview">Eventuali modifiche apportate ai flussi di dati della destinazione Pinterest (obsoleta) dopo il 16 novembre *non* vengono automaticamente trasferite alla nuova destinazione Pinterest. </span>
>Ad esempio, *non consigliare* che attivi nuovi tipi di pubblico nella vecchia destinazione dopo il 16 novembre. In tal caso, dovrà seguire la [passaggi di attivazione regolari](/help/destinations/ui/activate-segment-streaming-destinations.md) per aggiungere il pubblico alla nuova destinazione una volta intraprese le azioni del cliente.

**Entro il 15 dicembre 2023**: <span class="preview">Azione cliente 1</span>. È necessario eseguire nuovamente l&#39;autenticazione in Pinterest in modo che la nuova scheda sia collegata a Pinterest. Visualizzare le istruzioni complete in [questa sezione](#reauthenticate).

<span class="preview">Azione cliente 2</span>Quindi devi disattivare i flussi di dati verso Pinterest nella vecchia scheda e abilitare i flussi di dati nella nuova scheda. Visualizzare le istruzioni complete in [questa sezione](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Dopo il 18 gennaio 2024**: <span class="preview">Pinterest ha disattivato l’accesso all’API dell’inserzionista V4. Tutti i clienti Real-Time CDP che non hanno effettuato l’aggiornamento alla nuova destinazione troveranno i propri flussi di dati alla destinazione Pinterest che non riescono. [Autentica di nuovo in Pinterest](#reauthenticate) e [abilitare i flussi di dati](#disable-old-enable-new-flows) alla destinazione aggiornata per riprendere le campagne in Pinterest</span>.

## Altri elementi da annotare

Dopo aver abilitato i flussi di dati sulla nuova scheda di destinazione e aver disabilitato i flussi di dati sulle vecchie schede di destinazione, dovresti vedere nessuna interruzione nelle campagne o nel numero di profili qualificati nei tipi di pubblico provenienti da Adobe Real-Time CDP.
