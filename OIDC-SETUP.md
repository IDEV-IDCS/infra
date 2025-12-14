# OIDC Setup with Keycloak

## Services Supporting OIDC

### ✅ Confirmed OIDC Support
- **Plane** - Built-in OIDC via web UI
- **Grafana** - Native OIDC support
- **PostHog** - OIDC/SAML support

### ❌ No Native OIDC Support
- **Prometheus** - Basic auth only
- **Loki** - No built-in auth
- **Umami** - No OIDC support
- **Alloy** - No built-in auth

## Keycloak Client Configuration

### 1. Create Realm
- Realm: `devcode`
- Display name: `DevCode Services`

### 2. Create Clients

#### Plane Client
```
Client ID: plane
Client Type: OpenID Connect
Access Type: confidential
Valid Redirect URIs: https://plane.devcode.live/auth/oidc/callback/
Web Origins: https://plane.devcode.live
```

#### Grafana Client  
```
Client ID: grafana
Client Type: OpenID Connect
Access Type: confidential
Valid Redirect URIs: https://grafana.devcode.live/login/generic_oauth
Web Origins: https://grafana.devcode.live
```

#### PostHog Client
```
Client ID: posthog
Client Type: OpenID Connect
Access Type: confidential
Valid Redirect URIs: https://posthog.devcode.live/complete/oidc/
Web Origins: https://posthog.devcode.live
```

## Service Configuration

### Plane OIDC Setup
1. Deploy Plane
2. Go to `https://plane.devcode.live/god-mode/authentication/oidc`
3. Configure:
   - **Client ID**: `plane`
   - **Client Secret**: From Keycloak client
   - **Authorize URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/auth`
   - **Token URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/token`
   - **User Info URL**: `https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/userinfo`

### Grafana OIDC Setup
Add to Grafana environment:
```env
GF_AUTH_GENERIC_OAUTH_ENABLED=true
GF_AUTH_GENERIC_OAUTH_NAME=Keycloak
GF_AUTH_GENERIC_OAUTH_CLIENT_ID=grafana
GF_AUTH_GENERIC_OAUTH_CLIENT_SECRET=your-client-secret
GF_AUTH_GENERIC_OAUTH_AUTH_URL=https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/auth
GF_AUTH_GENERIC_OAUTH_TOKEN_URL=https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/token
GF_AUTH_GENERIC_OAUTH_API_URL=https://keycloak.devcode.live/realms/devcode/protocol/openid-connect/userinfo
GF_AUTH_GENERIC_OAUTH_SCOPES=openid profile email
```

### PostHog OIDC Setup
Add to PostHog environment:
```env
SOCIAL_AUTH_OIDC_OIDC_ENDPOINT=https://keycloak.devcode.live/realms/devcode
SOCIAL_AUTH_OIDC_KEY=posthog
SOCIAL_AUTH_OIDC_SECRET=your-client-secret
```

## Security Notes
- Use strong client secrets
- Enable PKCE where supported
- Configure proper redirect URIs
- Set up role-based access in Keycloak
- Use HTTPS for all endpoints
