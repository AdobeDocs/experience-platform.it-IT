---
title: Stripe
description: Scopri come acquisire i dati dei pagamenti dall’account di Stripe a Adobe Experience Platform
badge: Beta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>L&#39;origine [!DNL Stripe] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Migliaia di aziende di tutte le dimensioni utilizzano [!DNL Stripe] sia online che di persona per accettare pagamenti, generare nuove fonti di reddito ed espandersi a livello globale con l&#39;aiuto di Adobe Experience Platform, Adobe Commerce e [!DNL Magento Open Source].

Utilizza l&#39;origine [!DNL Stripe] in Experience Platform per acquisire i dati acquisiti dai tuoi clienti durante il flusso di acquisto. Una volta acquisiti, utilizza questi dati per creare offerte personalizzate e sbloccare informazioni aziendali più approfondite.

>[!TIP]
>
>Per domande sull&#39;origine [!DNL Stripe] nell&#39;Experience Platform, contattare [!DNL Stripe] all&#39;indirizzo adobe-partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Caso d&#39;uso di esempio per l&#39;origine [!DNL Stripe]**

La tua azienda consente ai clienti di acquistare oggetti nel tuo negozio online con l&#39;opzione di **acquistare adesso** e **pagare più tardi** (utilizzando [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] o [!DNL Zip]).

Utilizza l&#39;origine dati [!DNL Stripe] per analizzare l&#39;utilizzo delle opzioni **acquista ora** e **paga più tardi** e sperimentare offerte personalizzate per questi clienti. Ad esempio, si consiglia di aggiungere articoli per espandere il numero di articoli nel carrello prima del pagamento.

>[!ENDSHADEBOX]

Per informazioni su come configurare l&#39;account di origine [!DNL Stripe], recuperare le credenziali necessarie e creare gli schemi, leggere il documento seguente.

## Prerequisiti {#prerequisites}

Nelle sezioni seguenti vengono fornite informazioni sulla configurazione dei prerequisiti che è necessario completare prima di collegare l&#39;account [!DNL Stripe] all&#39;Experience Platform.

### Recuperare il token di accesso

* Accedi al [[!DNL Stripe] dashboard](https://dashboard.stripe.com/login) utilizzando l&#39;indirizzo e-mail e la password di [!DNL Stripe].
* Nel dashboard [!DNL Developers], selezionare **[!DNL API keys for developers]**.
* Nella scheda **Chiavi API**, seleziona **[!DNL Reveal test key]** per visualizzare il token di accesso.
* È ora possibile utilizzare questo token come token di accesso quando si connette l&#39;account [!DNL Stripe] a Experience Platform, utilizzando l&#39;API [!DNL Flow Service] o l&#39;interfaccia utente di Experience Platform.

### Raccogli le credenziali richieste

Per connettere l&#39;account [!DNL Stripe] a Experience Platform, è necessario fornire i valori per le credenziali di autenticazione seguenti:

>[!BEGINTABS]

>[!TAB API]

È necessario fornire le credenziali seguenti quando si connette l&#39;account [!DNL Stripe] utilizzando l&#39;API [!DNL Flow Service].

| Credenziali | Descrizione |
| --- | --- |
| `accessToken` | Token di autenticazione del codice di aggiornamento di [!DNL Stripe] OAuth 2. |
| `connectionSpec.id` | ID della specifica di connessione dell&#39;origine [!DNL Stripe]. Questo ID è corretto come: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB Interfaccia utente]

È necessario fornire le credenziali seguenti quando si connette l&#39;account [!DNL Stripe] tramite l&#39;interfaccia utente di Experience Platform.

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Token di autenticazione del codice di aggiornamento di [!DNL Stripe] OAuth 2. |

>[!ENDTABS]

Per ulteriori informazioni sull&#39;utilizzo delle API [!DNL Stripe], leggere la [[!DNL Stripe] documentazione sulle chiavi API](https://docs.stripe.com/keys).

### Creare uno schema Experience Data Model (XDM)

L&#39;origine [!DNL Stripe] supporta l&#39;acquisizione di dati dai percorsi di risorse seguenti:

* Spese
* Abbonamenti
* Rimborsi
* Transazioni saldo
* Clienti
* Prezzi

È necessario creare uno schema XDM per descrivere un set di dati, che può memorizzare i campi e i tipi di dati che verranno inviati da [!DNL Stripe] all&#39;Experience Platform.

>[!BEGINTABS]

>[!TAB Spese]

In [!DNL Stripe], **gli addebiti** rappresentano i tentativi di trasferire denaro in [!DNL Stripe]. Per ulteriori informazioni sugli attributi di addebito specifici, leggere la [[!DNL Stripe] guida API per le tariffe](https://docs.stripe.com/api/charges).

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

In [!DNL Stripe], puoi utilizzare **abbonamenti** per addebitare un cliente su base periodica. Per ulteriori informazioni sugli attributi di sottoscrizione specifici, consulta la [[!DNL Stripe] guida API sulle sottoscrizioni](https://docs.stripe.com/api/subscriptions).

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

In [!DNL Stripe], puoi utilizzare **rimborsi** per rimborsare un addebito creato in precedenza. Per ulteriori informazioni sugli attributi di rimborso specifici, consulta la [[!DNL Stripe] guida API sui rimborsi](https://docs.stripe.com/api/refunds).

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

In [!DNL Stripe], **transazioni saldo** rappresentano il movimento di fondi tra i tuoi account [!DNL Stripe]. Per ulteriori informazioni sugli attributi specifici delle transazioni saldo, leggere la [[!DNL Stripe] guida API sulle transazioni saldo](https://docs.stripe.com/api/balance_transactions).

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

In [!DNL Stripe], **clienti** rappresentano un determinato cliente della tua azienda. Per informazioni su attributi cliente specifici, leggere la [[!DNL Stripe] guida API sui clienti](https://docs.stripe.com/api/customers) per ulteriori informazioni su attributi cliente specifici.

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

In [!DNL Stripe], **i prezzi** rappresentano il costo unitario, la valuta e il ciclo di fatturazione facoltativo per l&#39;acquisto di prodotti sia ricorrente che occasionale. Per ulteriori informazioni sugli attributi di prezzo specifici, consulta la [[!DNL Stripe] guida API sui prezzi](https://docs.stripe.com/api/prices).

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

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account [!DNL Stripe] all&#39;Experience Platform, è necessario avere entrambe le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** abilitate per il proprio account. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

## Passaggi successivi

Dopo aver completato la configurazione dei prerequisiti, puoi procedere con la connessione e acquisire i dati di [!DNL Stripe] per Experience Platform. Leggi le seguenti guide per scoprire come acquisire i dati dei pagamenti [!DNL Stripe] per Experience Platform utilizzando le API o l&#39;interfaccia utente:

* [Acquisisci i dati dei pagamenti dall&#39;account di Stripe ad Experience Platform utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/payments/stripe.md).
* [Acquisisci i dati dei pagamenti dall&#39;account di Stripe ad Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/payments/stripe.md).
