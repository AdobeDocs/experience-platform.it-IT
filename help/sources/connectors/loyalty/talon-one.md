---
title: Panoramica di Talon.One Source
description: Scopri le fonti di Talon.One su Adobe Experience Platform
badge: Beta
exl-id: 92ed180a-6175-45e2-a831-0f40fd8606b0
source-git-commit: 3d0c216a9f8eb46a25221660253a80ce8e7a7eb0
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 2%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>Le origini [!DNL Talon.One] sono in versione beta. Leggi i [termini e condizioni](../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

Con [!DNL Talon.One] puoi creare, gestire e ottimizzare facilmente campagne di marketing personalizzate per i tuoi clienti. Utilizza questa potente piattaforma per applicare sconti, distribuire coupon, avviare programmi di riferimento, impostare programmi fedeltà e offrire incentivi gamified, il tutto da un unico sistema scalabile progettato per aiutare a coinvolgere e premiare il pubblico.

È possibile utilizzare le origini [!DNL Talon.One] nel catalogo delle origini di Adobe Experience Platform per acquisire sia i dati batch che i dati fedeltà in streaming dall&#39;account [!DNL Talon.One].

* [Eventi di streaming Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Connettore Source per batch Talon.One](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>I dati sulla fedeltà si riferiscono alle informazioni sul programma fedeltà degli utenti finali, ad esempio punti fedeltà, punti fedeltà spesi, livello corrente, coupon concessi, riferimenti e risultati.

## Prerequisiti {#prerequisites}

Specificare i valori per le credenziali seguenti per l&#39;autenticazione e la connessione a [!DNL Talon.One Batch Source Connector].

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Dominio | L&#39;URL univoco associato all&#39;ambiente dell&#39;applicazione [!DNL Talon.One]. Assicurati di non includere il protocollo o il percorso durante l’immissione del dominio. | `acmetalonone.us-east4` |
| Chiave API di gestione [!DNL Talon.One] | La chiave Management API è una credenziale utilizzata per autenticare e autorizzare l&#39;accesso all&#39;API Management di [!DNL Talon.One]. In questo modo vengono gestite operazioni quali: <ul><li>Importazione di coupon</li><li>Recupero dati campagna</li><li>Gestione di applicazioni ed endpoint</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## Mappatura {#mapping}

Per semplificare la mappatura di ogni oggetto effetto in base al relativo valore univoco `effectType`, è possibile utilizzare la funzione di preparazione dati `array_to_map`. Questo consente di convertire facilmente un array non ordinato di effetti in coppie chiave-valore corrispondenti alle proprie esigenze. Consulta l’esempio seguente per maggiori informazioni.

Puoi anche utilizzare i gruppi di campi fedeltà standardizzati forniti da Adobe per modellare i concetti del programma fedeltà in modo coerente.

>[!BEGINTABS]

>[!TAB Dettagli fedeltà]

Si tratta di un gruppo di campi XDM standard per il profilo individuale XDM, utilizzato per descrivere lo stato di iscrizione fedeltà di una persona acquisendo gli attributi del record anziché i dati dell’evento. Utilizza questo gruppo di campi negli schemi del profilo per acquisire:

* **Chi** il membro è nel programma (`loyaltyID`, `program`, `status`, `tier`)
* I relativi **saldi correnti e di durata** (`points`, `lifetimePoints`, `expiredPoints`, ecc.)
* Chiave **date appartenenza** (`joinDate`, `upgradeDate`, `tierExpiryDate`)

>[!TAB Dettagli evento fedeltà]

Il gruppo di campi Dettagli evento fedeltà è progettato per acquisire l’attività fedeltà a livello di evento, ad esempio i punti guadagnati o rimborsati in una transazione specifica. Questo gruppo di campi include campi come `xdm:points`, `xdm:pointsRedeemed`, `xdm:pointsAsOfDate` e `xdm:program`. Utilizza questo gruppo di campi a livello di evento negli schemi Experience Event per acquisire:

* **Movimenti per evento** in punti (ottenuti, riscattati, scaduti)
* **Sconti** guidati da coupon fedeltà o riferimenti
* **ID programma** e ID transazione per la riconciliazione con il provider fedeltà.

>[!ENDTABS]

| Origine | Destinazione |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## Passaggi successivi

Leggi la documentazione seguente per scoprire come collegare l&#39;account [!DNL Talon.One] ad Experience Platform e acquisire dati di fidelizzazione sia in batch che in streaming.

* [Eventi di streaming Talon.One](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Connettore Source per batch Talon.One](../../tutorials/ui/create/loyalty/talon-one-batch.md)
