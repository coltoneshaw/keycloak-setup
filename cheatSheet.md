
## Mattermost Config

<details>
  <summary>Mattermost SAML config</summary>
  
  ```json
    "SamlSettings": {
        "Enable": true,
        "EnableSyncWithLdap": false,
        "EnableSyncWithLdapIncludeAuth": false,
        "IgnoreGuestsLdapSync": false,
        "Verify": false,
        "Encrypt": false,
        "SignRequest": false,
        "IdpURL": "http://localhost:8080/realms/master/protocol/saml",
        "IdpDescriptorURL": "http://localhost:8080/realms/master",
        "IdpMetadataURL": "http://mattermost-meetup-keycloak:8080/realms/master/protocol/saml/descriptor",
        "ServiceProviderIdentifier": "mattermost",
        "AssertionConsumerServiceURL": "http://localhost:8065/login/sso/saml",
        "SignatureAlgorithm": "RSAwithSHA1",
        "CanonicalAlgorithm": "Canonical1.0",
        "ScopingIDPProviderId": "",
        "ScopingIDPName": "",
        "IdpCertificateFile": "saml-idp.crt",
        "PublicCertificateFile": "",
        "PrivateKeyFile": "",
        "IdAttribute": "",
        "GuestAttribute": "",
        "EnableAdminAttribute": false,
        "AdminAttribute": "",
        "FirstNameAttribute": "givenName",
        "LastNameAttribute": "surname",
        "EmailAttribute": "email",
        "UsernameAttribute": "username",
        "NicknameAttribute": "",
        "LocaleAttribute": "",
        "PositionAttribute": "",
        "LoginButtonText": "SAML",
        "LoginButtonColor": "#34a28b",
        "LoginButtonBorderColor": "#2389D7",
        "LoginButtonTextColor": "#ffffff"
    },

  ```
</details>

