````markdown
# 🚨 Aplicación Vulnerable para Prácticas de Seguridad DevSecOps

Este proyecto es una aplicación Node.js vulnerable, diseñada para practicar la integración de **herramientas de seguridad en pipelines CI/CD** y desplegar en **Heroku** mediante **Docker** y **GitHub Actions**.

---

## 🐳 Despliegue en Heroku con Docker (local y CI/CD)

### 1. Requisitos
- Cuenta en [Heroku](https://id.heroku.com/)
- Heroku CLI instalado
- Docker instalado
- Git configurado

### 2. Clonar o forkar este repositorio

```bash
git clone https://github.com/<tu-usuario>/vulnerable-web-app.git
cd vulnerable-web-app
````

### 3. Login en Heroku

```bash
heroku login
heroku container:login
```

### 4. Crear aplicación y configurar

```bash
heroku create <YOUR_APP_NAME>
heroku git:remote -a <YOUR_APP_NAME>
```

### 5. Build & Deploy manual (opcional)

```bash
heroku container:push web
heroku container:release web
heroku open
```

### 6. Ver logs

```bash
heroku logs --tail
```

---

## ⚙️ CI/CD Automatizado con GitHub Actions

### Configuración

1. Agrega tu **HEROKU\_API\_KEY** como `secret` en GitHub:

   * Ve a *Settings > Secrets and variables > Actions*
   * Agrega una nueva secret con nombre `HEROKU_API_KEY`

2. Verifica en `.github/workflows/deploy.yml` que estén configurados:

```yaml
heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
heroku_app_name: "nombre-de-tu-app"
heroku_email: "tu-email@ejemplo.com"
remote_branch: "master"
usedocker: true
```

---

## 🔐 Seguridad Integrada en CI/CD

Se añadieron herramientas automáticas para detectar vulnerabilidades y errores de seguridad en cada push:

### 1. **npm audit**

* Escanea dependencias npm por vulnerabilidades conocidas.
* Ejecutado en `.github/workflows/security-npm.yml`.

### 2. **CodeQL** (GitHub Native)

* Análisis estático del código JavaScript.
* Detecta errores de seguridad en el código fuente.
* Ejecutado en `.github/workflows/codeql.yml`.

### 3. **Trivy**

* Escaneo de vulnerabilidades y misconfiguraciones en la imagen Docker.
* Ejecutado en `.github/workflows/trivy.yml`.

### 4. **Gitleaks**

* Escanea el código fuente en busca de **secrets** o **claves expuestas**.
* Ejecutado en `.github/workflows/gitleaks.yml`.

> ✅ Todos los resultados pueden verse en la pestaña **Actions** de GitHub.

---

## 🧪 ¿Cómo correr escaneos manualmente?

Desde tu entorno local también podés ejecutar:

```bash
npm audit
trivy image nombre-de-la-imagen
gitleaks detect --source .
```

---

## 📌 Créditos

Proyecto original forkeado desde: [GinoDevOps/vulnerable-web-app](https://github.com/GinoDevOps/vulnerable-web-app)

---

## ✉️ Contacto

Pedro Echeverría – 2025
Desarrollado como parte del examen práctico final de DevSecOps.

```


