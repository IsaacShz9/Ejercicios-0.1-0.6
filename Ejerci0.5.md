```mermaid
sequenceDiagram
    participant U as Usuario
    participant B as Navegador
    participant S as Servidor

    U->>B: Navegar a /spa
    B->>S: GET /spa
    activate S
    S-->>B: HTML para la SPA
    deactivate S

    B->>S: GET /main.css
    activate S
    S-->>B: Archivo CSS
    deactivate S

    B->>S: GET /spa.js
    activate S
    S-->>B: Archivo JavaScript para SPA
    deactivate S

    Note right of B: El navegador ejecuta el código JavaScript de la SPA

    B->>S: GET /data.json
    activate S
    S-->>B: JSON con todas las notas [{ "content": "HTML is easy", "date": "2023-1-1" }, ... , { "content": "nueva nota", "date": "2024-6-16" }]
    deactivate S

    Note right of B: El navegador renderiza las notas usando el JSON recibido
