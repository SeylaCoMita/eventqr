# EventQR

Sistema de control de asistencia y registro de eventos (NiceGUI + SQLModel + PostgreSQL).

## Base de datos (Supabase)
1. `cp .env.example .env` y pega tu `DATABASE_URL` (Dashboard > Connect > Session pooler).
2. Las tablas se crean solas al arrancar. Luego, en el SQL Editor de Supabase, activa RLS:
   ```sql
   ALTER TABLE events ENABLE ROW LEVEL SECURITY;
   ALTER TABLE participants ENABLE ROW LEVEL SECURITY;
   ALTER TABLE attendances ENABLE ROW LEVEL SECURITY;
   ```

## Ejecutar
- Docker: `docker compose up --build` → http://localhost:8080
- Local: `pip install -r requirements.txt && python -m app.main`

## Check-in
En la pestaña **Check-in** hay tres formas de registrar asistencia:
1. **Cámara en vivo:** se abre sola al entrar a la pestaña y muestra el video en la página (botón "Activar/Detener cámara" y selector Trasera/Frontal). Requiere **HTTPS** (o `localhost`); los navegadores bloquean la cámara en `http://IP:puerto`.
2. **Lector USB:** el lector escribe el token y envía Enter.
3. **Manual:** pegar el token y pulsar Enter.

El escáner usa `html5-qrcode` 2.3.8 (Apache-2.0), incluido en `app/static/` y servido localmente: no depende de CDN.
