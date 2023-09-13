# Keycloak setup

This is a simple keycloak base to setup the environment with Mattermost. This already includes postgres and mattermost, however, if you're feeling adventurous use an existing deployment. 

## The Goal
Set up SAML authentication via Keycloak for Mattermost. You can find the docs [here](https://docs.mattermost.com/onboard/sso-saml-keycloak.html). You'll notice keycloak is v22 but the docs were written for v18. Keycloak still works and the docs remain _mostly_ the same. I've changed the keycloak version to give you a more real world of what customers face because 3rd party tools are updated far faster than we can keep up on docs. 

## To Start

1. Run `docker-compose up` / `docker compose up`
  - I like to keep logs in the console for this for your sanity during setup. You do you.
  - Keycloak can take 2-5 minutes to spin up. Check the logs for `Updating the configuration and installing your custom providers, if any. Please wait.` and if it's been more than 5 minutes just restart the container. 
2. Navigate to `localhost:8065` and create an account
3. Upload your enterprise license. 
4. Set System Console > Logging > FileInfo to debug (You will thank me later.)

## Logins

### Postgres
To access the database use `localhost:5432`
`mmuser` / `mmuser_password`

### Keycloak
To access the admin panel go to `localhost:8080`
`admin` / `admin`

## Notes

- This is a docker setup and keycloak does not love docker. If the container gets stuck turning on, force stope it and start it again. Sometimes just a restart will fix it. No rhyme or reason.
- OpenLDAP is also included, if you need it. It will automatically enable you to utilize the precreated profiles. 
- local mode is already enabled for you. You can access it via
  ```
  docker exec -it cs-repro-mattermost mmctl 
  ```
- Signed responses **is not reliable with keycloak**. I would keep it turned off, and that's our stance to customers too for keycloak. If you can figure out how to enable it consistently please document it and let us know. You'll win the award of appreciation! The greatest honor.
- Set everything up with no encryption first, to confirm it works and remove a variable. Once it all works, go about enabling encryption.
- To use `Get SAML Metadata from Idp` you need to set `ServiceSettings.AllowedUntrustedInternalConnections = 'mattermost-meetup-keycloak:8080 mattermost-meetup-keycloak'`. Then restart.
  - Note that once you import the meta data adjust the `SAML SSO URL` and `Identify Provider Issuer URL` to be `localhost` instead of `mattermost-meetup-keycloak`.
- If you're lost adding the additional attributes they are at Keycloak > Clients > Mattermost > Client Scopes. Then click `Mattermost-dedicated`. 
  - You'll need to add the predefined mappers and create `username` and `id` mappers (add mapper > by configuration > User Attribute )
- If you're curious what attributes are available check `http://localhost:8080/realms/master/protocol/saml/descriptor` . 
- I was struggling with the ID attribute on this for SAML, so feel free to leave that one blank.
- A zip file of keycloak exists in the root of this, in the event you need to reset keycloak and not lose your mattermost config. 