
```mermaid
sequenceDiagram
    participant U as Usuario
    participant B as Navegador
    participant S as Servidor

    Note right of U: El usuario escribe una nota en el campo de texto
    U->>B: Hacer clic en el botón "Save"
    
    B->>S: POST /new_note con el contenido de la nueva nota
    activate S
    Note right of S: El servidor recibe la nueva nota y la guarda en la base de datos
    S-->>B: 302 Found (Redirigir a /notes)
    deactivate S

    B->>S: GET /notes
    activate S
    S-->>B: Documento HTML con las notas
    deactivate S

    B->>S: GET /main.css
    activate S
    S-->>B: Archivo CSS
    deactivate S

    B->>S: GET /main.js
    activate S
    S-->>B: Archivo JavaScript
    deactivate S

    Note right of B: El navegador ejecuta el código JavaScript que obtiene el JSON del servidor

    B->>S: GET /data.json
    activate S
    S-->>B: JSON con todas las notas [{ "content": "HTML is easy", "date": "2023-1-1" }, ... , { "content": "nueva nota", "date": "2024-6-16" }]
    deactivate S

    Note right of B: El navegador ejecuta la función de callback que renderiza las notas, incluida la nueva nota
