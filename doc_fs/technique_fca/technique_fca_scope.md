
# Comment utiliser les scopes OpenID Connect pour accéder aux données des utilisateurs ? 

## Scope et Claims dans OpenID Connect

### Qu'est ce qu'un scope dans OpenID Connect ? 

> Les clients OpenID Connect utilisent des *scopes* tels que définis dans la section 3.3 de [OAuth 2.0 [RFC6749]](https://openid.net/specs/openid-connect-basic-1_0.html#RFC6749) pour spécifier quels privilèges d'accès sont demandés pour les *access token*. Les *scopes* associées aux *access token* déterminent les ressources qui seront disponibles lorsqu'elles sont utilisées pour accéder aux *endpoints* protégés par OAuth 2.0. Pour OpenID Connect, les *scopes* peuvent être utilisées pour demander que des ensembles d'informations spécifiques soient mis à disposition en tant que *claims*.

*Source: [OpenID Connect Basic Client Implementer's Guide 1.0](https://openid.net/specs/openid-connect-basic-1_0.html#Scopes)*

Le protocole OpenID Connect défini un certain nombre de [scopes standards](https://openid.net/specs/openid-connect-basic-1_0.html#Scopes) qu'il est possible d'étendre avec des *scopes* spécifiques supplémentaires en fonction du besoin de l'*identity provider*.

*En bref :* Les scopes permettent de définir l'ensemble des informations à disposition du Fournisseur de Services pour une cinématique. 

### Qu'est ce qu'un claim dans OpenID Connect ? 

Dans OpenId Connect, un claim est une information relative à l'utilisateur ou à la phase l'authentification. Ces informations peuvent être disponibles soit dans l'ID Token, soit dans la réponse du UserInfo. Les claims retournés dans ces jetons dépendent des scopes associés à l'*access token*. 

Le protocole OpenId Connect defini un certain nombre de [claims standards](https://openid.net/specs/openid-connect-core-1_0.html#Claims).

*En Bref :* Les claims sont les informations sur l'utilisateur ou la phase d'authentification disponible dans l'ID Token ou dans la réponse de UserInfo. 

## Les scopes et les claims dans AgentConnect

### Liste des claims 

### Les données d'identité obligatoires

|Champs | Obligatoire | Description| Format |
|---- | ------ | ------ | ------ |
|given_name | Oui |Prénoms séparés par des espaces (standard OpenIDConnect)| UTF-8 (standard OpenIDConnect)|
|usual_name| Oui |Nom de famille d'usage (par défaut = family_name)| UTF-8 |
|email | Oui |Adresse courriel |UTF-8 (standard OpenIDConnect)|
|uid|Oui |Identifiant unique de l'agent auprès du FI| String (standard OpenIDConnect)|

L'uid est une donnée technique qui ne peut pas être demandé par le Fournisseur de Services.

En complément, il est possible d'obtenir des données complémentaires. Cependant ces données ne sont pas obligatoirement connues par tous les Fournisseurs d'Identité.


### Les données complémentaires

Champs | Obligatoire | Description| Format |
|---- | ------ | ------ | ------ |
| siren | non  | Identifiant d'entreprise  | String, 9 chiffres sans espace |
| siret | non |Identifiant d'établissement| string, 14 chiffres sans espace|
| organizational_unit  | non  | Ministère/Direction/Service d'affectation   | UTF8 |
| belonging_population  | non  | Population d'appartenance  | string, Exemple: agent, prestataire, partenaire, stagiaire |
| phone  | non  | Téléphones de contact  | Format non normé |
| chorusdt   | Non | Entité ministérielle/Matricule Agent  | string |

La liste des données complémentaires est non exhaustive et pourra être amendée si besoin.


AgentConnect transmet systématiquement au Fournisseur de Services un identifiant unique pour chaque agent : 

* Cet identifiant est spécifique à chaque Fournisseur de Services. Un même utilisateur aura donc un identifiant unique différent pour chacun des Fournisseurs de Services auxquels il accède. 

### Les données sur l'authentification

Les claims relatifs à l'authentification disponible par AgentConnect sont des claims standards et sont disponible uniquement dans l'ID Token. Ces claims sont les suivants : 

- amr
- acr
- sid
- auth_time
- iss

[Plus d'informations sur ces claims](https://openid.net/specs/openid-connect-basic-1_0.html#IDToken)

### Correspondance entre scope et claims sur AgentConnect

Le tableau suivant décris la liste des *claims* accessible en fonction des *scopes* associés à l'access token.

| Scope       | Claims   |
| --- | --- |
| openid | sub |
| given_name | given_name|
| usual_name| usual_name |
| email | email |
| uid | uid|
| siren | siren |
| siret | siret |
| organizational_unit | organizational_unit |
| belonging_population | belonging_population |
| phone | phone_number |
| chorusdt | chorusdt:matricule, chorusdt:societe |
| idp_id | idp_id|
| idp_acr | idp_acr|

---

Voir aussi : 
- [Quel est le détail du fonctionnement ?](../fonctionnement_fca/details_fonctionnement.md)
- [Quels sont les endpoints sur AgentConnect (le contrat d'API) ?](../technique_fca/endpoints.md)
- [Quelles sont les données que je peux récupérer par AgentConnect sur les agents ?](../projet_fca/projet_fca_donnees.md)
- [Quelles sont les données d'AgentConnect qui expirent ?](../technique_fca/donnees_expirent.md)
- [Qu'est ce qu'eIDAS et quel est le niveau de garantie d'AgentConnect ?](../projet_fca/projet_fca_niveau_eidas.md)