# Mini Guía de Jorge para usar Graph API y generar permisos a invitados



# GRAPH EXPLORER
Para hacer todas las pruebas de forma rápida y sencilla, usamos GRAPH EXPLORER:

https://developer.microsoft.com/en-us/graph/graph-explorer

También se puede usar Postman/Insomnia, pero el Graph Explorer es cómodo para la autenticación (no tenemos que preocuparnos de renovar token ni nada por el estilo)



# Cómo obtener la autenticación por UiPath

Se obtiene el token usando HTTP Request con client id + tenant + secret:

```json
POST https://login.microsoftonline.com/b234bc80-a99d-4a47-8071-62b90ee1479b/oauth2/v2.0/token

https://login.microsoftonline.com/{tenant_id}/oauth2/v2.0/token

X URL FORM ENCODED

client_id : {application id}
scope : https://graph.microsoft.com/.default
client_secret : {client secret}
grant_type : client_credentials


Response:

{
	"token_type": "Bearer",
	"expires_in": 3599,
	"ext_expires_in": 3599,
	"access_token": "eyJ0eXAiOiJKV1QiLCJub25jZSI6Ik5LZURvWHluNWlhRC1zNl9LdW5xZms3OEhNTGlEVVpHNVN4ZUhLWTRlcHciLCJhbGciOiJSUzI1NiIsIng1dCI6Ii1LSTNROW5OUjdiUm9meG1lWm9YcWJIWkdldyIsImtpZCI6Ii1LSTNROW5OUjdiUm9meG1lWm9YcWJIWkdldyJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLm1pY3Jvc29mdC5jb20iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9iMjM0YmM4MC1hOTlkLTRhNDctODA3MS02MmI5MGVlMTQ3OWIvIiwiaWF0IjoxNjg2NzUzODAwLCJuYmYiOjE2ODY3NTM4MDAsImV4cCI6MTY4Njc1NzcwMCwiYWlvIjoiRTJaZ1lGakp6dHlXS0phdCtxZnE2Q3A1bFlPRkFBPT0iLCJhcHBfZGlzcGxheW5hbWUiOiJVSVBBVEgiLCJhcHBpZCI6ImU5OTUwNGZiLTI5OGItNGI5Mi1hMDI5LWMwYjFkOGYzM2MwZiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0L2IyMzRiYzgwLWE5OWQtNGE0Ny04MDcxLTYyYjkwZWUxNDc5Yi8iLCJpZHR5cCI6ImFwcCIsIm9pZCI6IjYzZjc4OTc2LTY5NTItNGI0OC1iMWFjLWUzODU5Zjg3MmNlOCIsInJoIjoiMC5BUXdBZ0x3MHNwMnBSMHFBY1dLNUR1Rkhtd01BQUFBQUFBQUF3QUFBQUFBQUFBQ1dBQUEuIiwicm9sZXMiOlsiTWFpbC5SZWFkV3JpdGUiLCJVc2VyLlJlYWRXcml0ZS5BbGwiLCJNYWlsLlJlYWRCYXNpYy5BbGwiLCJEaXJlY3RvcnkuUmVhZFdyaXRlLkFsbCIsIk1haWxib3hTZXR0aW5ncy5SZWFkIiwiU2l0ZXMuUmVhZC5BbGwiLCJTaXRlcy5SZWFkV3JpdGUuQWxsIiwiRmlsZXMuUmVhZFdyaXRlLkFsbCIsIkRpcmVjdG9yeS5SZWFkLkFsbCIsIlVzZXIuUmVhZC5BbGwiLCJGaWxlcy5SZWFkLkFsbCIsIk1haWwuUmVhZCIsIk1haWwuU2VuZCIsIk1haWxib3hTZXR0aW5ncy5SZWFkV3JpdGUiLCJNYWlsLlJlYWRCYXNpYyJdLCJzdWIiOiI2M2Y3ODk3Ni02OTUyLTRiNDgtYjFhYy1lMzg1OWY4NzJjZTgiLCJ0ZW5hbnRfcmVnaW9uX3Njb3BlIjoiRVUiLCJ0aWQiOiJiMjM0YmM4MC1hOTlkLTRhNDctODA3MS02MmI5MGVlMTQ3OWIiLCJ1dGkiOiJmT09jN3hVNlpreTFLeDQ1SzIxdkFBIiwidmVyIjoiMS4wIiwid2lkcyI6WyIwOTk3YTFkMC0wZDFkLTRhY2ItYjQwOC1kNWNhNzMxMjFlOTAiXSwieG1zX3RjZHQiOjE0MjU5MjU0MDcsInhtc190ZGJyIjoiRVUifQ.VVbyYqlTn9RfCsjxGme-9t6SMZybn6OmJJ-kYkl4fvROCjSbqiVO0rlyuisxh3VDyweHszEIx389Aw7gepiRwuCq1QYEwPDRmttU_LOgWIKhSWcSG18CiD-ZzH-RW8Bi7RF3PmAoHnLnqvdZE_su0OCcUt2yPC__nGgIc7wkGJgQlcRq5yaCpVz8YItHwXMiF2kt9yM9t77pIgHSEJPd8P5n3qmiiHju2wtDYNHhHrTW7BBL20hob999VWIQkO2Dx0xUX-kXfs8rXKHUQk3nfY7UYPSITCSW6z3FQqj7hDfzxjGVwkoI5iWHLUaw_WiY1m96eMVNM0aiPC9BgIg4Ew"
}

```

En el resto de llamadas hay que añadir el header de Authorization: "Bearer {token}"

# Usuario:


Servicios.Financiero1RPA@clarkemodet.com
XJMUMPGd8sWKTP


URL Base del Sharepoint: https://clarkemodetcloud.sharepoint.com/sites/Shared/RPA

# Grupo

Se ha creado el grupo "COEIF" para asociar usuarios a él. No es 100% necesario usarlo pero por buenas prácticas estaría bien asignar los usuarios a dicho grupo:

## Get User Groups
```json
GET https://graph.microsoft.com/v1.0/me/transitiveMemberOf/microsoft.graph.group?$count=true

RESPONSE (cropped)

        {
            "id": "435cb23d-bf76-4890-996a-f7bca74c8785",
            "deletedDateTime": null,
            "classification": null,
            "createdDateTime": "2023-05-12T08:13:41Z",
            "creationOptions": [],
            "description": null,
            "displayName": "Grgs_SP_RPA_COEIF",
            "expirationDateTime": null,
            "groupTypes": [],
            "isAssignableToRole": null,
            "mail": null,
            "mailEnabled": false,
            "mailNickname": "Grgs_SP_RPA_COEIF",
            "membershipRule": null,
            "membershipRuleProcessingState": null,
            "onPremisesDomainName": "Clarkemodet.grupo",
            "onPremisesLastSyncDateTime": "2023-05-12T08:13:41Z",
            "onPremisesNetBiosName": "CLARKEMODET",
            "onPremisesSamAccountName": "Grgs_SP_RPA_COEIF",
            "onPremisesSecurityIdentifier": "S-1-5-21-2128310829-2099726424-2028992-61687",
            "onPremisesSyncEnabled": true,
            "preferredDataLocation": null,
            "preferredLanguage": null,
            "proxyAddresses": [],
            "renewedDateTime": "2023-05-12T08:13:41Z",
            "resourceBehaviorOptions": [],
            "resourceProvisioningOptions": [],
            "securityEnabled": true,
            "securityIdentifier": "S-1-12-1-1130148413-1217445750-3170331289-2240236711",
            "theme": null,
            "visibility": null,
            "onPremisesProvisioningErrors": []
        },

```

Lo importantes es el id

## Get Users belonging to group (COEIF)

Con el id podemos comprobar los miembros:

```json
GET https://graph.microsoft.com/v1.0/groups/435cb23d-bf76-4890-996a-f7bca74c8785/members

RESPONSE:
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#directoryObjects",
    "value": [
        {
            "@odata.type": "#microsoft.graph.user",
            "id": "1342e286-14c4-4cad-8427-a1e1d9606338",
            "businessPhones": [],
            "displayName": "Servicios.Financiero1RPA",
            "givenName": "Servicios.Financiero1RPA",
            "jobTitle": null,
            "mail": "Servicios.Financiero1RPA@clarkemodet.com",
            "mobilePhone": null,
            "officeLocation": null,
            "preferredLanguage": null,
            "surname": null,
            "userPrincipalName": "Servicios.Financiero1RPA@clarkemodet.com"
        }
    ]
}
```

# Files and folders

Para asignar los permisos primero tenemos que encontrar el ID del archivo/carpeta, ambos se obtienen de la misma forma y tienen un ID asociado.

EJEMPLO: Buscamos el archivo "RPA2PRUEBA" en todo el sharepoint

```json
POST https://graph.microsoft.com/v1.0/search/query
Body:
{
    "requests": [
        {
            "entityTypes": [
                "driveItem"
            ],
            "query": {
                "queryString": "RPA2PRUEBA"
            }
        }
    ]
}



RESPONSE:

{
    "value": [
        {
            "searchTerms": [
                "rpa2prueba"
            ],
            "hitsContainers": [
                {
                    "hits": [
                        {
                            "hitId": "01QNW2GLRVK32ZBPX6RBELBEXUM7PMACPI",
                            "rank": 1,
                            "summary": "/* miércoles, 11 de enero de 202315:19:11 User: RPA_BBDD_UserPre Server: BIPROCM0001 Database: ProcesosRPA_UiPath_PRE Application: */ PEPTI_Main<ddd/>",
                            "resource": {
                                "@odata.type": "#microsoft.graph.driveItem",
                                "size": 344,
                                "fileSystemInfo": {
                                    "createdDateTime": "2023-05-11T13:28:59Z",
                                    "lastModifiedDateTime": "2023-05-11T13:28:59Z"
                                },
                                "listItem": {
                                    "@odata.type": "#microsoft.graph.listItem",
                                    "fields": {},
                                    "id": "90f55635-febe-4888-b092-f467dec009e8"
                                },
                                "id": "01QNW2GLRVK32ZBPX6RBELBEXUM7PMACPI",
                                "createdBy": {
                                    "user": {
                                        "displayName": "Servicios.Financiero1RPA",
                                        "email": "servicios.financiero1rpa@clarkemodet.com"
                                    }
                                },
                                "createdDateTime": "2023-05-11T13:28:59Z",
                                "lastModifiedBy": {
                                    "user": {
                                        "displayName": "Servicios.Financiero1RPA",
                                        "email": "servicios.financiero1rpa@clarkemodet.com"
                                    }
                                },
                                "lastModifiedDateTime": "2023-05-11T13:28:59Z",
                                "name": "RPA2PRUEBA.txt",
                                "parentReference": {
                                    "driveId": "b!Q3CNXgoarkW7qfmBo8itF1tcex-FZg9Cnyfb7hGqByfipnrj5f8QSqEZp0CvdYtz",
                                    "id": "01QNW2GLTXYWQX4B4YKBCJK6A3TMNIRFBQ",
                                    "sharepointIds": {
                                        "listId": "e37aa6e2-ffe5-4a10-a119-a740af758b73",
                                        "listItemId": "7716",
                                        "listItemUniqueId": "90f55635-febe-4888-b092-f467dec009e8"
                                    },
                                    "siteId": "clarkemodetcloud.sharepoint.com,5e8d7043-1a0a-45ae-bba9-f981a3c8ad17,1f7b5c5b-6685-420f-9f27-dbee11aa0727"
                                },
                                "webUrl": "https://clarkemodetcloud.sharepoint.com/sites/Shared/RPA/COEDF/RPAJORGEPRUEBA/RPA2PRUEBA.txt"
                            }
                        }
                    ],
                    "total": 1,
                    "moreResultsAvailable": false
                }
            ]
        }
    ],
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#Collection(microsoft.graph.searchResponse)"
}
```

NOTA: existen más parámetros posibles para la query de búsqueda, pero con el nombre debería ser suficiente. Lo importante nuevamente es el ID: en este caso es suficiente con el "hitID" ```01QNW2GLRVK32ZBPX6RBELBEXUM7PMACPI``` (valor único para cada archivo/carpeta)

El DriveID también es importante pero no debería cambiar para el sharepoint indicado (/Shared/RPA): ```b!Q3CNXgoarkW7qfmBo8itF1tcex-FZg9Cnyfb7hGqByfipnrj5f8QSqEZp0CvdYtz/items/01QNW2GLS6FSNKDZSDLJAJFPYD5AKMAI6F/invite```

# Usuarios

Para poder darle permisos a un usuario que no estuviera ya en el dominio tenemos que hacer dos llamadas:

## Invitar nuevo usuario (externo) a ClarkeModet
```json
POST https://graph.microsoft.com/v1.0/invitations
Body:
{
    "invitedUserEmailAddress": "jorge.caravaca@asesormasmovil.es",
    "inviteRedirectUrl": "https://google.es"
}

RESPONSE:
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#invitations/$entity",
    "id": "e9848418-2915-43c8-a6d0-16ab8dbcd37c",
    "inviteRedeemUrl": "https://login.microsoftonline.com/redeem?rd=https%3a%2f%2finvitations.microsoft.com%2fredeem%2f%3ftenant%3db234bc80-a99d-4a47-8071-62b90ee1479b%26user%3de9848418-2915-43c8-a6d0-16ab8dbcd37c%26ticket%3dqAa78d6hpbFF81W4FAG%25252b2U7rAtpZwE9dze3F%25252fJmMu98%25253d%26ver%3d2.0",
    "invitedUserDisplayName": null,
    "invitedUserType": "Guest",
    "invitedUserEmailAddress": "jorge.caravaca@asesormasmovil.es",
    "sendInvitationMessage": false,
    "resetRedemption": false,
    "inviteRedirectUrl": "https://google.es/",
    "status": "PendingAcceptance",
    "invitedUserMessageInfo": {
        "messageLanguage": null,
        "customizedMessageBody": null,
        "ccRecipients": [
            {
                "emailAddress": {
                    "name": null,
                    "address": null
                }
            }
        ]
    },
    "invitedUser": {
        "id": "625b381b-42e8-421d-b8db-7ebe34f4cf1c"
    }
}
```

Nuevamente lo importante es el id de invitedUser.


## Usuario ya existente
Podemos buscar el usuario así:

```json
GET https://graph.microsoft.com/v1.0/users?$filter=userType eq 'Guest' and mail eq 'jmcaravaca@minsait.com'

El 'Guest' técnicamente no es necesario, es sólo para filtrar los invitados

Sin Body

Response:

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users",
    "value": [
        {
            "businessPhones": [],
            "displayName": "Caravaca Vidal, Jorge Manuel",
            "givenName": null,
            "jobTitle": null,
            "mail": "jmcaravaca@minsait.com",
            "mobilePhone": null,
            "officeLocation": null,
            "preferredLanguage": null,
            "surname": null,
            "userPrincipalName": "jmcaravaca_minsait.com#EXT#@clarkemodetcloud.onmicrosoft.com",
            "id": "4c2685b9-9dbb-4b9f-ba11-79a91d2617cf"
        }
    ]
}

De aquí podemos sacar ya el ID (si fuera necesario) o simplemente comprobar que ya está dado de alta en el dominio
```


# Dar acceso al usuario

## Dar acceso a carpeta/archivo

```json
POST https://graph.microsoft.com/v1.0/drives/b!Q3CNXgoarkW7qfmBo8itF1tcex-FZg9Cnyfb7hGqByfipnrj5f8QSqEZp0CvdYtz/items/01QNW2GLS6FSNKDZSDLJAJFPYD5AKMAI6F/invite

La url es de tipo /drives/{drive-id}/items/{item-id}/invite

Body
{
    "recipients": [
        {
            "email": "jorge.caravaca@asesormasmovil.es"
        }
    ],
    "message": "Here's the file that we're collaborating on.",
    "requireSignIn": true,
    "roles": [
        "write"
    ]
}


Response:

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#Collection(permission)",
    "value": [
        {
            "@odata.type": "#microsoft.graph.permission",
            "id": "aTowIy5mfG1lbWJlcnNoaXB8am1jYXJhdmFjYV9taW5zYWl0LmNvbSNleHQjQGNsYXJrZW1vZGV0Y2xvdWQub25taWNyb3NvZnQuY29t",
            "roles": [
                "write"
            ],
            "grantedTo": {
                "user": {
                    "email": "jmcaravaca@minsait.com",
                    "id": "4c2685b9-9dbb-4b9f-ba11-79a91d2617cf",
                    "displayName": "Caravaca Vidal, Jorge Manuel"
                }
            }
        }
    ]
}
```

Con esto el usuario ya tiene permiso para ver la carpeta/archivo, pero tenemos que generar un link. Aunque es posible que se pueda hacer con actividades de UiPath, también se puede hacer por API:


```json
https://graph.microsoft.com/v1.0/drives/b!Q3CNXgoarkW7qfmBo8itF1tcex-FZg9Cnyfb7hGqByfipnrj5f8QSqEZp0CvdYtz/items/01QNW2GLS6FSNKDZSDLJAJFPYD5AKMAI6F/createLink


La url es de tipo /drives/{drive-id}/items/{item-id}/createLink

BODY:

{
    "type": "edit",
    "scope": "users"
}


{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#permission",
    "@odata.type": "#microsoft.graph.permission",
    "id": "f3d45a95-e5dc-422e-85f2-2104ec38de1c",
    "roles": [
        "read"
    ],
    "shareId": "u!aHR0cHM6Ly9jbGFya2Vtb2RldGNsb3VkLnNoYXJlcG9pbnQuY29tLzpmOi9zL1NoYXJlZC9FbDRzbXFIbVExcEFrcjhENkJUQUk4VUJQUlYzSC1qd2JZazZhNmJXRTdBRE53",
    "hasPassword": false,
    "grantedToIdentitiesV2": [
        {
            "user": {
                "@odata.type": "#microsoft.graph.sharePointIdentity",
                "displayName": "María Díez",
                "email": "mdiez@Clarkemodet.com",
                "id": "b157fe59-a051-47ae-b4ee-0ff47b9eacc2"
            },
            "siteUser": {
                "displayName": "María Díez",
                "email": "mdiez@Clarkemodet.com",
                "id": "439",
                "loginName": "i:0#.f|membership|mdiez@clarkemodet.com"
            }
        }
    ],
    "grantedToIdentities": [
        {
            "user": {
                "displayName": "María Díez",
                "email": "mdiez@Clarkemodet.com",
                "id": "b157fe59-a051-47ae-b4ee-0ff47b9eacc2"
            }
        }
    ],
    "link": {
        "scope": "users",
        "type": "view",
        "webUrl": "https://clarkemodetcloud.sharepoint.com/:f:/s/Shared/El4smqHmQ1pAkr8D6BTAI8UBPRV3H-jwbYk6a6bWE7ADNw",
        "preventsDownload": false
    }
}
```

La URL está en webURL





# Licencias

## Listar licencias de usuario


```json

GET https://graph.microsoft.com/v1.0/users/bcc26e71-4823-4c28-94f3-ed41ae63a852/licenseDetails

URL es https://graph.microsoft.com/v1.0/users/{user_id}}/licenseDetails

Sin Body

Response:

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('bcc26e71-4823-4c28-94f3-ed41ae63a852')/licenseDetails",
    "value": [
        {
            "id": "gLw0sp2pR0qAcWK5DuFHm8zrA6Tg-qJMjIx6kH_WwjU",
            "skuId": "a403ebcc-fae0-4ca2-8c8c-7a907fd6c235",
            "skuPartNumber": "POWER_BI_STANDARD",
            "servicePlans": [
                {
                    "servicePlanId": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "servicePlanName": "EXCHANGE_S_FOUNDATION",
                    "provisioningStatus": "Success",
                    "appliesTo": "Company"
                },
                {
                    "servicePlanId": "2049e525-b859-401b-b2a0-e0a31c4b1fe4",
                    "servicePlanName": "BI_AZURE_P0",
                    "provisioningStatus": "Success",
                    "appliesTo": "User"
                }
            ]
        }
    ]
}



```

De aquí lo importante son los "skuId" de cada elemento del value (value es un array de elementos, es decir, de licencias) para luego poder quitar la licencia


## Asignar licencia (quitar y/o poner)

```json

POST https://graph.microsoft.com/v1.0/users/bcc26e71-4823-4c28-94f3-ed41ae63a852/assignLicense

URL es https://graph.microsoft.com/v1.0/users/{user_id}}/assignLicense

{
    "addLicenses": [],
    "removeLicenses": [
        "a403ebcc-fae0-4ca2-8c8c-7a907fd6c235"
    ]
}

Response:

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users/$entity",
    "businessPhones": [],
    "displayName": "Ricky He",
    "givenName": "Ricky He",
    "jobTitle": "Operations trainee",
    "mail": null,
    "mobilePhone": null,
    "officeLocation": "Rio de Janeiro",
    "preferredLanguage": null,
    "surname": "He",
    "userPrincipalName": "rhe@clarkemodetcloud.onmicrosoft.com",
    "id": "bcc26e71-4823-4c28-94f3-ed41ae63a852"
}


Si la licencia no estuviera asignada, devuelve un 400:


{
    "error": {
        "code": "Request_BadRequest",
        "message": "User does not have a corresponding license.",
        "innerError": {
            "date": "2023-06-14T08:55:17",
            "request-id": "a8735d07-fff4-46e7-ad65-05906abcd50f",
            "client-request-id": "50d497ad-25bd-f2f1-868b-b34a5d9662a4"
        }
    }
}


```
El body tiene que incluir ambas keys aunque esté vacío (en el ejmplo, sólo quitamos una licencia)


# Groups

## Listar Grupos del usuario

```json
GET  https://graph.microsoft.com/v1.0/users/bcc26e71-4823-4c28-94f3-ed41ae63a852/memberOf

URL es https://graph.microsoft.com/v1.0/users/{user_id}/memberOf



Response:

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#directoryObjects",
    "value": [
        {
            "@odata.type": "#microsoft.graph.group",
            "id": "c785150c-5d23-4dd5-a33e-389e98559c8d",
            "deletedDateTime": null,
            "classification": null,
            "createdDateTime": "2021-11-10T15:45:02Z",
            "creationOptions": [],
            "description": null,
            "displayName": "Grgs_ES_Team",
            "expirationDateTime": null,
            "groupTypes": [],
            "isAssignableToRole": null,
            "mail": null,
            "mailEnabled": false,
            "mailNickname": "Grgs_ES_Team",
            "membershipRule": null,
            "membershipRuleProcessingState": null,
            "onPremisesDomainName": "Clarkemodet.grupo",
            "onPremisesLastSyncDateTime": "2023-06-14T08:23:10Z",
            "onPremisesNetBiosName": "CLARKEMODET",
            "onPremisesSamAccountName": "Grgs_ES_Team",
            "onPremisesSecurityIdentifier": "S-1-5-21-2128310829-2099726424-2028992-59628",
            "onPremisesSyncEnabled": true,
            "preferredDataLocation": null,
            "preferredLanguage": null,
            "proxyAddresses": [],
            "renewedDateTime": "2021-11-10T15:45:02Z",
            "resourceBehaviorOptions": [],
            "resourceProvisioningOptions": [],
            "securityEnabled": true,
            "securityIdentifier": "S-1-12-1-3347387660-1305828643-2654486179-2375832984",
            "theme": null,
            "visibility": null,
            "onPremisesProvisioningErrors": []
        },
        {
            "@odata.type": "#microsoft.graph.group",
            "id": "9e48a453-2dd7-48c8-9b3e-d86f37d1e74a",
            "deletedDateTime": null,
            "classification": null,
            "createdDateTime": "2021-11-10T15:45:02Z",
            "creationOptions": [],
            "description": null,
            "displayName": "Grgs_CTO_Corporate",
            "expirationDateTime": null,
            "groupTypes": [],
            "isAssignableToRole": null,
            "mail": null,
            "mailEnabled": false,
            "mailNickname": "Grgs_CTO_Corporate",
            "membershipRule": null,
            "membershipRuleProcessingState": null,
            "onPremisesDomainName": "Clarkemodet.grupo",
            "onPremisesLastSyncDateTime": "2023-06-14T08:23:10Z",
            "onPremisesNetBiosName": "CLARKEMODET",
            "onPremisesSamAccountName": "Grgs_CTO_Corporate",
            "onPremisesSecurityIdentifier": "S-1-5-21-2128310829-2099726424-2028992-59626",
            "onPremisesSyncEnabled": true,
            "preferredDataLocation": null,
            "preferredLanguage": null,
            "proxyAddresses": [],
            "renewedDateTime": "2021-11-10T15:45:02Z",
            "resourceBehaviorOptions": [],
            "resourceProvisioningOptions": [],
            "securityEnabled": true,
            "securityIdentifier": "S-1-12-1-2655560787-1221078487-1876442779-1256706359",
            "theme": null,
            "visibility": null,
            "onPremisesProvisioningErrors": []
        },
        {
            "@odata.type": "#microsoft.graph.group",
            "id": "4f2c24e3-3f59-41f6-adbe-8516c977a9ef",
            "deletedDateTime": null,
            "classification": null,
            "createdDateTime": "2021-12-27T12:56:19Z",
            "creationOptions": [],
            "description": "Acceso 2F al portal de Citrix (NetScaler). Si el usuario tiene 2F activado en Office 365, le saltará el doble factor. Si no, le solicitará credenciales sin doble factor. La pertenencia a este grupo es requisito obligatorio para todos los usuarios que tengan que autenticarse por 2F para acceder al portal de Citrix.",
            "displayName": "CTXACC_PRO",
            "expirationDateTime": null,
            "groupTypes": [],
            "isAssignableToRole": null,
            "mail": null,
            "mailEnabled": false,
            "mailNickname": "CTXACC_PRO",
            "membershipRule": null,
            "membershipRuleProcessingState": null,
            "onPremisesDomainName": "Clarkemodet.grupo",
            "onPremisesLastSyncDateTime": "2023-06-14T08:23:10Z",
            "onPremisesNetBiosName": "CLARKEMODET",
            "onPremisesSamAccountName": "CTXACC_PRO",
            "onPremisesSecurityIdentifier": "S-1-5-21-2128310829-2099726424-2028992-60241",
            "onPremisesSyncEnabled": true,
            "preferredDataLocation": null,
            "preferredLanguage": null,
            "proxyAddresses": [],
            "renewedDateTime": "2021-12-27T12:56:19Z",
            "resourceBehaviorOptions": [],
            "resourceProvisioningOptions": [],
            "securityEnabled": true,
            "securityIdentifier": "S-1-12-1-1328293091-1106657113-377863853-4020860873",
            "theme": null,
            "visibility": null,
            "onPremisesProvisioningErrors": []
        }
    ]
}
```
Tenemos un array de los grupos, para luego quitar los grupos tenemos que coger los id de cada elemento (el Id de usuario también lo necesitaremos)

## Check user in group

```json

https://graph.microsoft.com/v1.0/groups/4f2c24e3-3f59-41f6-adbe-8516c977a9ef/members?$count=true&$filter=userPrincipalName eq 'rhe@clarkemodetcloud.onmicrosoft.com'



```


## Quitar grupos

No funciona por Graph para la mayoría de grupos -> Los de Active Directory se quitan desde active directory, y los de "mail" (listas de distribución) se quitan desde Exchange


# Mailbox/AutoReply

## Comprobar Autoreply

```json

GET https://graph.microsoft.com/v1.0/users/bcc26e71-4823-4c28-94f3-ed41ae63a852/mailboxSettings

users/{userid}/mailboxSettings

RESPONSE:
{
	"@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('bcc26e71-4823-4c28-94f3-ed41ae63a852')/mailboxSettings",
	"archiveFolder": "AQMkAGViNDY5Yjc4LTQxZTEtNDM2NS04MGRjLWMxODFhNzYwZWI1YQAuAAADEoK1AdBX-kGb9HAbeosvKwEATwhdCs1nGECDOB1s1lu4ZQAAAgETAAAA",
	"delegateMeetingMessageDeliveryOptions": "sendToDelegateOnly",
	"userPurpose": "user",
	"automaticRepliesSetting": {
		"status": "disabled",
		"externalAudience": "all",
		"internalReplyMessage": "",
		"externalReplyMessage": "",
		"scheduledStartDateTime": {
			"dateTime": "2023-06-14T14:00:00.0000000",
			"timeZone": "UTC"
		},
		"scheduledEndDateTime": {
			"dateTime": "2023-06-15T14:00:00.0000000",
			"timeZone": "UTC"
		}
	},
	"language": {},
	"workingHours": {}
}
```

## Set Autoreply

```json
PATCH https://graph.microsoft.com/v1.0/users/bcc26e71-4823-4c28-94f3-ed41ae63a852/mailboxSettings

users/{user-id}/mailboxSettings
(Igual que el de GET)

BODY:

{
	"automaticRepliesSetting": {
		"status": "alwaysEnabled",
		"externalAudience": "all",
		"internalReplyMessage": "Hola, estoy de vacaciones",
		"externalReplyMessage": "Hola, estoy de vacaciones"
	}
}

RESPONSE:

Igual que el Get
```

Dentro del body ponemos las keys que queremos cambiar, en principio, con cambiar el status y los mensajes debería ser suficiente. Si hay que ponerlo programado, el status es scheduled

# Docs

https://developer.microsoft.com/en-us/graph/graph-explorer

https://learn.microsoft.com/en-us/graph/use-the-api?context=graph%2Fapi%2F1.0&view=graph-rest-1.0

https://stackoverflow.com/questions/68863841/microsoft-graph-create-share-link-for-specific-people