# Industry Standard: Federation
*Notes on this video https://videos.pingidentity.com/detail/videos/identity-standards/video/1017466745001/industry-standard:-federation?sort_by=PUBLISH_DATE%3AASC*

## SSO
 - Multiple applications are available as a result of signing onto one of them.
 - Achieved via a session cookie valid visible to all apps served from *.example.com.
 - EG: Logon ont GMail and subsequently have access to GDocs
 - However, people often use the term SSO to refer to a more general solution than this (see below)

## Federation
 - One repository of credentials is used by multiple applications
 - Uses still need to logon to each application seperately but one one repository is used

## Identity Federation
*AKA : "Internet Single sign-On" or "Internet SSO" or "Identity Federation"*

 - Authenticate the user once and share that identity between multiple domain
 - The result is that users can access applications on any of the domains with out having to log on again.
 - The Identity Provider (iDp) is the entity that authenticates the user and asserts their identity to other systems.
 - The Service Provider (SP) is the application or system that relies on the IdP’s authentication rather than handling passwords directly.
   - This works because the SP has already decided they will trust iDp to authenticate users .
 - The iDp issues something to the User (you could think of it as a drivers licences) and all SPs (who have agreed to) will considered that good enough to consider the User trustable (like all bars would consider a Drivers License indication that you should be trusted).

### Authnetication Flow
 - The User tries to access a SP ("Company B")
 - The SP redirects the user to the the iDP.
