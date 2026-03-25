---
title: Migrazione della destinazione Pinterest alla nuova API. Azione del cliente richiesta.
description: Pinterest sta rendendo obsoleta l’API dell’inserzionista v4 attualmente utilizzata dalla destinazione Pinterest in Real-Time CDP. Scopri le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Aggiornamento della destinazione Pinterest alla nuova API. Azione cliente richiesta entro il 18 gennaio 2024.

>[!IMPORTANT]
>
>Gli elementi azione cliente in questa pagina sono applicabili se l&#39;organizzazione ha impostato flussi di dati per esportare dati in Pinterest prima del 16 novembre 2023, data in cui la nuova destinazione **[!UICONTROL Pinterest]**, utilizzando l&#39;API Pinterest più recente, è stata aggiunta al catalogo delle destinazioni.

## Cosa succede? {#what-is-happening}

Pinterest ha dichiarato obsoleta l&#39;API pubblicitaria v4 utilizzata dalla [destinazione Pinterest](/help/destinations/catalog/advertising/pinterest.md) in [!DNL Real-Time CDP]. Adobe ha aggiornato la destinazione per l&#39;utilizzo dell&#39;API pubblicitaria [v5](https://developers.pinterest.com/docs/getting-started/migration/). Leggi questa pagina per comprendere le azioni da eseguire per passare facilmente alla nuova API senza interrompere le campagne Pinterest.

## Perché mi viene inviata una notifica? {#why-notified}

Abbiamo identificato la tua organizzazione come dotata di flussi di dati attivi per attivare i tipi di pubblico in Pinterest.

## Qual è il piano? {#what-is-the-plan}

Adobe ha rilasciato una nuova scheda di destinazione Pinterest che sfrutta l’API Pinterest v5 e manterrà i flussi di dati esistenti nella nuova connessione.

## Devo fare qualcosa per mantenere attivi i tipi di pubblico? {#action-required}

Sì, prima del 18 gennaio 2024, è necessario eseguire l&#39;autenticazione nella nuova destinazione Pinterest con l&#39;account dell&#39;inserzionista Pinterest in [!DNL Real-Time CDP]. Consulta le istruzioni dettagliate di seguito.

### Autentica di nuovo in Pinterest {#reauthenticate}

1. Vai a **[!UICONTROL Destinations > Accounts]** e utilizza il filtro sullo schermo per filtrare solo la destinazione Pinterest.
   ![Filtra solo account Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Nella destinazione **Pinterest**, selezionare il simbolo dei tre punti ... e selezionare **[!UICONTROL Edit details]**.
   ![Seleziona Modifica dettagli](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Seleziona **[!UICONTROL Reconnect OAuth]** e accedi al tuo account Pinterest.
   ![Seleziona Riconnetti OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Passa all’azione nella sezione seguente

### Abilita i flussi nella nuova destinazione {#disable-old-enable-new-flows}

Quindi devi abilitare i flussi di dati alla nuova scheda **[!UICONTROL Pinterest]**.

1. Vai a **[!UICONTROL Destinations > Browse]** e utilizza il filtro sullo schermo per filtrare solo la destinazione **[!UICONTROL Pinterest]**.
   ![Filtrare i flussi di dati di Pinterest solo nella scheda Sfoglia](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Seleziona il nome della connessione ipertestuale (campagna fedeltà nell&#39;esempio della schermata precedente) alla destinazione **[!UICONTROL Pinterest]** e cambia **[!UICONTROL Enable]** in **on**.
   ![Attiva per le nuove connessioni e disattiva per le connessioni precedenti](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Puoi condividere alcune timeline di alto livello? {#high-level-timelines}

Sì, vedi di seguito:

**Entro il 16 novembre 2023**: la nuova destinazione è pronta e dovresti vedere due schede Pinterest una accanto all&#39;altra nel catalogo fino a quando Pinterest non smette di supportare la vecchia API v4. Tutti i flussi di dati esistenti nella scheda Pinterest corrente vengono copiati nella nuova destinazione.

![affiancata la destinazione Pinterest precedente e quella nuova](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**Entro il 15 dicembre 2023**: <span class="preview">Azione cliente 1</span>. È necessario eseguire nuovamente l&#39;autenticazione in Pinterest in modo che la nuova scheda sia collegata a Pinterest. Visualizza istruzioni complete in [questa sezione](#reauthenticate).

<span class="preview">Azione cliente 2</span>. È quindi necessario abilitare i flussi di dati nella nuova scheda. Visualizza istruzioni complete in [questa sezione](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Dopo il 18 gennaio 2024**: <span class="preview">Pinterest ha disattivato l&#39;accesso all&#39;API dell&#39;inserzionista V4. Tutti i clienti [!DNL Real-Time CDP] che non hanno effettuato l&#39;aggiornamento alla nuova destinazione troveranno i propri flussi di dati alla destinazione Pinterest con errori. [Esegui nuovamente l&#39;autenticazione in Pinterest](#reauthenticate) e [abilita i flussi di dati](#disable-old-enable-new-flows) nella destinazione aggiornata per riprendere le campagne in Pinterest.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
