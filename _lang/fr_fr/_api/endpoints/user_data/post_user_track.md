---
nav_title: "POST : Suivi utilisateur"
article_title: "POST : Suivi utilisateur"
search_tag: Endpoint
page_order: 4
layout: api_page
page_type: reference
description: "Cet article présente en détail l’endpoint Braze Suivi utilisateur."

---
{% api %}
# Suivi utilisateur
{% apimethod post core_endpoint|https://www.braze.com/docs/core_endpoints %}
/users/track
{% endapimethod %}

> Utilisez ce point de terminaison pour enregistrer des événements et des achats personnalisés et mettre à jour les attributs du profil utilisateur.

{% alert note %}
Braze traite les données transmises via l’API à leur valeur nominale et les clients ne devraient transmettre des deltas (modification des données) que pour minimiser la consommation inutile de points de données. Pour en savoir plus, consultez Points de données[]({{site.baseurl}}/user_guide/data_and_analytics/data_points/).
{% endalert %}

{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#4cf57ea9-9b37-4e99-a02e-4373c9a4ee59 {% endapiref %}

## Conditions préalables

Pour utiliser cet endpoint, vous aurez besoin d'une [clé API]({{site.baseurl}}/api/api_key/) avec l’autorisation `users.track`.

Les clients utilisant l'API pour les appels de serveur à serveur devront peut-être inscrire `rest.iad-01.braze.com` dans la liste des autorisations s'ils sont derrière un pare-feu.

## Limite de débit

{% multi_lang_include rate_limits.md endpoint='users track' %}

## Corps de la demande

```
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
```

```json
{
  "attributes": (optional, array of attributes object),
  "events": (optional, array of event object),
  "purchases": (optional, array of purchase object),
}
```

### Paramètres de demande

{% alert important %}
Pour chaque composant de requête répertorié dans le tableau suivant, l'un des éléments suivants est requis : `external_id`, `user_alias`, `braze_id`, `email` ou `phone`.
{% endalert %}

| Paramètre | Requis | Type de données | Description |
| --------- | ---------| --------- | ----------- |
| `attributes` | Facultatif | Tableau d'objets d'attributs | Voir [l'objet Attributs utilisateur]({{site.baseurl}}/api/objects_filters/user_attributes_object/) |
| `events` | Facultatif | Tableau d'objets événementiels | Voir [l'objet événements]({{site.baseurl}}/api/objects_filters/event_object/) |
| `purchases` | Facultatif | Tableau d'objets d'achat | Voir [Objet Achats]({{site.baseurl}}/api/objects_filters/purchase_object/) |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Exemple de requêtes

### Mettre à jour un profil utilisateur par adresse e-mail

À l’aide de l’endpoint `/users/track`, vous pouvez mettre à jour un profil utilisateur par adresse e-mail. 

```
curl --location --request POST 'https://rest.iad-01.braze.com/users/track' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
    "attributes": [
        {
            "email": "test@braze.com",
            "string_attribute": "fruit",
            "boolean_attribute_1": true,
            "integer_attribute": 25,
            "array_attribute": [
                "banana",
                "apple"
            ]
        }
    ],
    "events": [
        {
            "email": "test@braze.com",
            "app_id": "your_app_identifier",
            "name": "rented_movie",
            "time": "2022-12-06T19:20:45+01:00",
            "properties": {
                "release": {
                    "studio": "FilmStudio",
                    "year": "2022"
                },
                "cast": [
                    {
                        "name": "Actor1"
                    },
                    {
                        "name": "Actor2"
                    }
                ]
            }
        },
        {
            "user_alias": {
                "alias_name": "device123",
                "alias_label": "my_device_identifier"
            },
            "app_id": "your_app_identifier",
            "name": "rented_movie",
            "time": "2013-07-16T19:20:50+01:00"
        }
    ],
    "purchases": [
        {
            "email": "test@braze.com",
            "app_id": "your_app_identifier",
            "product_id": "product_name",
            "currency": "USD",
            "price": 12.12,
            "quantity": 6,
            "time": "2017-05-12T18:47:12Z",
            "properties": {
                "color": "red",
                "monogram": "ABC",
                "checkout_duration": 180,
                "size": "Large",
                "brand": "Backpack Locker"
            }
        }
    ]
}'
```

### Mettre à jour un profil utilisateur par numéro de téléphone

Vous pouvez mettre à jour un profil utilisateur par numéro de téléphone en utilisant l’endpoint `/users/track`. Ce point de terminaison ne fonctionne que si vous incluez un numéro de téléphone valide.

{% alert important %}
Si vous incluez une demande à la fois par e-mail et par téléphone, Braze utilisera l'e-mail comme identifiant.
{% endalert %}

```
curl --location --request POST 'https://rest.iad-01.braze.com/users/track' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
    "attributes": [
        {
            "phone": "+15043277269",
            "string_attribute": "fruit",
            "boolean_attribute_1": true,
            "integer_attribute": 25,
            "array_attribute": [
                "banana",
                "apple"
            ]
        }
    ],
}'
```
### Définir des groupes d'abonnement

Cet exemple montre comment créer un utilisateur et définir son groupe d'abonnement dans l'objet d'attributs utilisateur. 

La mise à jour du statut d’abonnement avec cet endpoint mettra à jour l’utilisateur spécifié par son `external_id` (comme User1) et mettre à jour le statut de l’abonnement de tous les utilisateurs ayant le même e-mail que cet utilisateur (Utilisateur1).

```
curl --location --request POST 'https://rest.iad-01.braze.com/users/track' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
  "attributes": [
  {
    "external_id": "user_identifier",
    "email": "example@email.com",
    "email_subscribe": "subscribed",
    "subscription_groups": [{
      "subscription_group_id": "subscription_group_identifier_1",
      "subscription_state": "unsubscribed"
      },
      {
        "subscription_group_id": "subscription_group_identifier_2",
        "subscription_state": "subscribed"
        },
        {
          "subscription_group_id": "subscription_group_identifier_3",
          "subscription_state": "subscribed"
        }
      ]
    }
  ]
}'
```

### Exemple de requête pour créer un utilisateur alias uniquement.

Vous pouvez utiliser l’endpoint `/users/track` pour créer un nouvel utilisateur alias uniquement en définissant la clé `_update_existing_only` avec une valeur `false` dans le corps de la requête. Si cette valeur est omise, le profil utilisateur alias uniquement ne sera pas créé. Un utilisateur alias uniquement permet de s’assurer qu’un seul profil avec cet alias existe. C’est notamment utile lorsque vous construisez une nouvelle intégration, car cela empêche la création de doublons de profil utilisateur

```
curl --location --request POST 'https://rest.iad-01.braze.com/users/track' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_REST_API_KEY' \
--data-raw '{
{
    "attributes": [
        {
            "_update_existing_only": false,
            "user_alias": {
                "alias_name": "example_name",
                "alias_label": "example_label"
            },
            "email": "email@example.com"
        }
    ],
}'
```


## Réponses

Lorsque vous utilisez l'une des requêtes API mentionnées ci-dessus, vous devriez recevoir l'une des trois réponses générales suivantes : un [message réussi](#successful-message), un [message réussi avec des erreurs non fatales](#successful-message-with-non-fatal-errors)ou un [message avec des erreurs fatales](#message-with-fatal-errors).

### Message réussi

Les messages réussis seront envoyés avec la réponse suivante :

```json
{
  "message": "success",
  "attributes_processed": (optional, integer), if attributes are included in the request, this will return an integer of the number of external_ids with attributes that were queued to be processed,
  "events_processed": (optional, integer), if events are included in the request, this will return an integer of the number of events that were queued to be processed,
  "purchases_processed": (optional, integer), if purchases are included in the request, this will return an integer of the number of purchases that were queued to be processed,
}
```

### Message réussi sans erreurs fatales

Si votre message est réussi, mais qu’il y a des erreurs non fatales, comme un objet Événement non valide hors d’une longue liste d’événements, vous recevrez la réponse suivante :

```json
{
  "message": "success",
  "errors": [
    {
      <minor error message>
    }
  ]
}
```

Pour les messages de réussite, toutes les données non affectées par une erreur dans le tableau `errors` continueront d’être traitées. 

### Message avec erreurs fatales

Si votre message contient une erreur fatale, vous recevrez la réponse suivante :

```json
{
  "message": <fatal error message>,
  "errors": [
    {
      <fatal error message>
    }
  ]
}
```

### Codes de réponse des erreurs fatales

Pour les codes de statut et les messages d’erreur associés qui seront renvoyés si votre demande rencontre une erreur fatale, consultez la section []({{site.baseurl}}/api/errors/#fatal-errors)Erreurs fatales et réponses.

Si vous recevez l'erreur « à condition que l'id\_externe soit sur liste noire et non autorisé », votre demande peut avoir inclus un « utilisateur factice ». Pour plus d’informations, consultez []({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_archival/#spam-blocking)Blocage des courriers indésirables. 

## Foire aux questions

### Que se passe-t-il lorsque plusieurs profils avec la même adresse e-mail sont trouvés ?
Si l’`external_id` existe, le profil le plus récemment mis à jour avec un ID externe sera utilisé en priorité pour les mises à jour. Si l’`external_id` n’existe pas, le profil le plus récemment mis à jour sera utilisé en priorité pour les mises à jour.

### Que se passe-t-il si aucun profil avec l’adresse e-mail n’existe actuellement ?
Un nouveau profil sera créé ainsi qu’un utilisateur par e-mail uniquement. Aucun alias ne sera créé. Le champ e-mail sera défini sur test@braze.com, comme indiqué dans l’exemple de requête pour mettre à jour un profil utilisateur par adresse e-mail.

### Comment utiliser `/users/track` pour importer des données utilisateur héritées ?
Vous pouvez soumettre des données via l'API Braze pour un utilisateur qui n'a pas encore utilisé votre application mobile pour générer un profil utilisateur. Si l’utilisateur se sert ultérieurement de l’application, toutes les informations qui suivent son identification via le SDK seront fusionnées avec le profil utilisateur existant que vous avez créé via l’appel d’API. Tout comportement utilisateur enregistré de manière anonyme par le SDK avant l'identification sera perdu lors de la fusion avec le profil utilisateur généré par l'API existant.

L’outil de segmentation inclura ces utilisateurs, qu’ils aient utilisé l’application ou pas. Si vous souhaitez exclure les utilisateurs téléchargés via l’API utilisateur qui n’ont pas encore utilisé l’application, ajoutez simplement le filtre : `Session Count > 0`.

### Comment `/users/track` gère-t-il les événements en double ?

Chaque objet événement du tableau événements représente une occurrence unique d'un événement personnalisé par un utilisateur à un moment donné. Cela signifie que chaque événement ingéré dans Braze possède son propre ID d'événement, de sorte que les événements « en double » sont traités comme des événements distincts et uniques.

{% endapi %}