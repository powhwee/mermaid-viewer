# Mermaid Viewer

A simple web-based viewer for Mermaid diagrams.  Mermaid code are often generated in AI code assistants which are useful diagrams.  This serves as an alternative to using the mermaid website to render diagrams, which has a limit if you save your diagram online. 

## How to use

1.  Open the `index.html` file in your web browser.
2.  Paste your Mermaid code into the text area.
3.  Click the "Render" button to see the rendered diagram.

## Deployed Website

You can deploy this simply to a cloud provider object storage since this is a static website and start using it!

Or save the index.html locally and open it.

## Test data

Sample sequence diagram code:

```
sequenceDiagram
    autonumber
    participant U as User
    participant B as Browser or App
    participant C as Client App
    participant A as Authorization Server
    participant R as Resource Server

    Note over C: Generate code_verifier and code_challenge (PKCE)

    U->>B: Click Sign in with Provider
    B->>A: GET /authorize<br/>client_id, redirect_uri, response_type=code, scope, code_challenge, code_challenge_method=S256, state
    A-->>U: Login and consent UI
    U->>A: Authenticate and consent
    A-->>B: 302 redirect to redirect_uri with code and state
    B->>C: Deliver authorization code

    C->>A: POST /token<br/>grant_type=authorization_code, code, redirect_uri, client_id, code_verifier
    A-->>C: Token response<br/>access_token, refresh_token (optional), expires_in, token_type

    C->>R: API request<br/>Authorization header Bearer access_token
    R-->>C: Protected resource
    C-->>U: Signed in session or data

    Note over C,A: Later refresh<br/>POST /token with grant_type=refresh_token
```

Screenshot of viewer:

![Viewer](screenshot/screenshot.png "Viewer")
