# Culto — Control Financiero

App web para el control financiero interno de Culto Running Crew.

## Tecnologías
- HTML/CSS/JS puro (sin frameworks)
- Firebase Firestore (base de datos en la nube)
- Firebase Authentication (login con Google)
- GitHub Pages (hosting gratuito)

---

## Configuración inicial (solo se hace una vez)

### 1. Reglas de seguridad en Firestore

En la consola de Firebase → Firestore → pestaña "Reglas", pegá esto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

Esto permite acceso solo a usuarios autenticados con Google.

### 2. Autorizar el dominio de GitHub Pages

En Firebase → Authentication → Settings → "Authorized domains"
Agregá: `TU-USUARIO.github.io`

### 3. Agregar socios autorizados (opcional pero recomendado)

En `index.html`, buscá esta sección:

```javascript
const ALLOWED_EMAILS = [
  // "socio1@gmail.com",
  // "socio2@gmail.com",
];
```

Descomentá y agregá los correos de los socios. Si el array está vacío, cualquier cuenta Google puede entrar.

---

## Subir a GitHub Pages

1. Creá un repositorio en GitHub llamado `culto-finanzas`
2. Subí el archivo `index.html` al repo
3. En Settings → Pages → Source: seleccioná `main` branch, carpeta `/ (root)`
4. GitHub te dará una URL tipo: `https://TU-USUARIO.github.io/culto-finanzas`

---

## Uso

- Cada socio entra con su cuenta Google
- Los datos se guardan en Firestore y son visibles para todos en tiempo real
- Exportar a CSV disponible en la pestaña Historial
- Tipos de registro: Ingresos, Gastos/Facturas, Inversiones
- Módulo separado para control de inventario de Merch
