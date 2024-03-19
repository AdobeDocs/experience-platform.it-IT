---
title: Stripe
description: Scopri come acquisire i dati dei pagamenti dall’account di Stripe a Adobe Experience Platform
badge: Beta
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>Il [!DNL Stripe] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Migliaia di aziende di tutte le dimensioni utilizzano [!DNL Stripe] sia online che di persona, per accettare pagamenti, generare nuove fonti di reddito ed espandersi a livello globale con l&#39;aiuto di Adobe Experience Platform, Adobe Commerce e [!DNL Magento Open Source].

Utilizza il [!DNL Stripe] origine in Experienci Platform per acquisire i dati acquisiti dai clienti durante il flusso di acquisto. Una volta acquisiti, utilizza questi dati per creare offerte personalizzate e sbloccare informazioni aziendali più approfondite.

>[!TIP]
>
>Per domande su [!DNL Stripe] sorgente su Experience Platform, contatto [!DNL Stripe] presso adobe-partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Caso d’uso di esempio per [!DNL Stripe] sorgente**

La tua azienda consente ai clienti di acquistare articoli nel tuo negozio online con l’opzione di **acquista ora** e **paghi più tardi** (utilizzando [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm], o [!DNL Zip]).

Utilizza il [!DNL Stripe] origine dati per analizzare l&#39;utilizzo di **acquista ora** e **paghi più tardi** opzioni e sperimenta offerte personalizzate per questi clienti. Ad esempio, si consiglia di aggiungere articoli per espandere il numero di articoli nel carrello prima del pagamento.

>[!ENDSHADEBOX]

Per informazioni su come impostare il [!DNL Stripe] dell&#39;account di origine, recuperare le credenziali necessarie e creare gli schemi.

## Prerequisiti {#prerequisites}

Nelle sezioni seguenti vengono fornite informazioni sulla configurazione dei prerequisiti che è necessario completare prima di connettere il [!DNL Stripe] da Experience Platform.

### Recuperare il token di accesso

* Accedi a [[!DNL Stripe] dashboard](https://dashboard.stripe.com/login) utilizzando [!DNL Stripe] indirizzo e-mail e password.
* In [!DNL Developers] dashboard, seleziona **[!DNL API keys for developers]**.
* Sotto **Chiavi API** , seleziona **[!DNL Reveal test key]** per visualizzare il token di accesso.
* È ora possibile utilizzare questo token come token di accesso durante la connessione [!DNL Stripe] da Experience Platform, utilizzando [!DNL Flow Service] o l’interfaccia utente di Experienci Platform.

### Raccogli le credenziali richieste

Per collegare il tuo [!DNL Stripe] account per Experience Platform, è necessario fornire i valori per le seguenti credenziali di autenticazione:

>[!BEGINTABS]

>[!TAB API]

È necessario fornire le seguenti credenziali quando si connette il [!DNL Stripe] account che utilizza [!DNL Flow Service] API.

| Credenziali | Descrizione |
| --- | --- |
| `accessToken` | Il tuo [!DNL Stripe] Token di autenticazione codice di aggiornamento OAuth 2. |
| `connectionSpec.id` | ID della specifica di connessione [!DNL Stripe] sorgente. Questo ID viene corretto come: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB Interfaccia utente]

È necessario fornire le seguenti credenziali quando si connette il [!DNL Stripe] tramite l’interfaccia utente di Experienci Platform.

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Il tuo [!DNL Stripe] Token di autenticazione codice di aggiornamento OAuth 2. |

>[!ENDTABS]

Per ulteriori informazioni sull’utilizzo di [!DNL Stripe] API, leggi [[!DNL Stripe] documentazione sulle chiavi API](https://docs.stripe.com/keys).

### Creare uno schema Experience Data Model (XDM)

Il [!DNL Stripe] l’origine supporta l’acquisizione di dati dai seguenti percorsi di risorse:

* Spese
* Abbonamenti
* Rimborsi
* Transazioni saldo
* Clienti
* Prezzi

Devi creare uno schema XDM per descrivere un set di dati, che può memorizzare i campi e i tipi di dati che verranno inviati da [!DNL Stripe] all&#39;Experience Platform.

>[!BEGINTABS]

>[!TAB Spese]

In entrata [!DNL Stripe], **spese** rappresenta i tentativi di trasferire denaro nel tuo [!DNL Stripe]. Leggi le [[!DNL Stripe] Guida API per le spese](https://docs.stripe.com/api/charges) per ulteriori informazioni su attributi di addebito specifici.

+++Selezionare per visualizzare l&#39;oggetto Stripe addebito

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Abbonamenti]

In entrata [!DNL Stripe], è possibile utilizzare **abbonamenti** per addebitare un cliente su base periodica. Leggi le [[!DNL Stripe] Guida API agli abbonamenti](https://docs.stripe.com/api/subscriptions) per ulteriori informazioni su attributi di abbonamento specifici.

+++Selezionare questa opzione per visualizzare l&#39;oggetto Stripe sottoscrizione

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Rimborsi]

In entrata [!DNL Stripe], è possibile utilizzare **rimborsi** per rimborsare un addebito creato in precedenza. Leggi le [[!DNL Stripe] Guida API ai rimborsi](https://docs.stripe.com/api/refunds) per ulteriori informazioni su attributi di rimborso specifici.

+++Selezionare per visualizzare l&#39;oggetto Stripe rimborso

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Transazioni saldo]

In entrata [!DNL Stripe], **saldi transazioni** rappresenta il movimento di fondi tra [!DNL Stripe] account. Leggi le [[!DNL Stripe] Guida API per le transazioni di saldo](https://docs.stripe.com/api/balance_transactions) per ulteriori informazioni sugli attributi specifici delle transazioni saldi.

+++Selezionare questa opzione per visualizzare l&#39;oggetto transazione saldo Stripe

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Clienti]

In entrata [!DNL Stripe], **clienti** rappresentare un determinato cliente della tua azienda. Per informazioni su attributi cliente specifici, leggi [[!DNL Stripe] Guida API per i clienti](https://docs.stripe.com/api/customers) per ulteriori informazioni su attributi cliente specifici.

+++Selezionare questa opzione per visualizzare l&#39;oggetto Stripe cliente

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Prezzi]

In entrata [!DNL Stripe], **prezzi** rappresenta il costo unitario, la divisa e il ciclo di fatturazione opzionale per l&#39;acquisto di prodotti sia ricorrente che occasionale. Leggi le [[!DNL Stripe] Guida API sui prezzi](https://docs.stripe.com/api/prices) per ulteriori informazioni su attributi di prezzo specifici.

+++Selezionare per visualizzare l&#39;oggetto Prezzo Stripe

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

### Configurare le autorizzazioni su Experienci Platform

Devi avere entrambi **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** autorizzazioni abilitate per il tuo account per connettersi al tuo [!DNL Stripe] da Experience Platform. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere [guida all’interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

## Passaggi successivi

Dopo aver completato la configurazione dei prerequisiti, puoi procedere con la connessione e l’acquisizione di [!DNL Stripe] dati di Experience Platform. Leggi le seguenti guide per scoprire come acquisire [!DNL Stripe] dati di pagamento da Experience Platform tramite API o l’interfaccia utente:

* [Acquisire i dati dei pagamenti dal proprio account di Stripe per Experienci Platform utilizzando l’API del servizio Flow](../../tutorials/api/create/payments/stripe.md).
* [Acquisire i dati dei pagamenti dall’account di Stripe ad Experienci Platform utilizzando l’interfaccia utente](../../tutorials/ui/create/payments/stripe.md).