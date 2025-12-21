# 📦 Repositorio de Aplicaciones Vue 3 (con Git Submodules)

Este repositorio funciona como un **contenedor de aplicaciones Vue 3**.
Cada aplicación vive en su **propio repositorio independiente** y se integra aquí mediante **Git Submodules**.

Repositorio principal:
👉 https://github.com/facundo-moran/repositorio-vue-3-vite

---

## 🧠 ¿Qué es un Git Submodule?

Un **submodule** es una referencia a **otro repositorio Git** dentro de este repositorio.

- Cada app tiene:
  - su propio historial
  - su propio `package.json`
  - su propio deploy
- Este repo **NO guarda el código de las apps**
- Solo guarda **el commit exacto** al que apunta cada app

📌 El repo padre **no copia archivos**, solo **apunta a commits**.

---

## 📁 Estructura del repositorio

```txt
repositorio-vue-3-vite/
├── .gitmodules
├── chat-tailwind/        ← submodule (app Vue)
├── otra-app/             ← submodule
└── README.md

Cada carpeta de app es un repo Git real, no una carpeta común.
```
---

## 🚀 Clonar el repositorio (IMPORTANTE)

### Para clonar correctamente este repo con sus apps:

```sh
$ git clone --recurse-submodules https://github.com/facundo-moran/repositorio-vue-3-vite
```
### Si ya clonaste sin submodules:
```sh
git submodule update --init --recursive
```

## ➕ Cómo agregar una nueva app como submodule

```txt
⚠️ Regla de oro:
La carpeta NO debe existir antes.
```
### Paso a paso

```sh
$ git submodule add <URL_DEL_REPO> <nombre-carpeta>
$ git commit -m "add <nombre-carpeta> as submodule"
$ git push

```
### Ejemplo real

```git
git submodule add https://github.com/facundo-moran/vue-3-vite-chat-tailwind chat-tailwind
git commit -m "add chat-tailwind app"
```

---
## ✍️ Cómo trabajar en una app (día a día)

### Entrar al submodule:
```sh
cd chat-tailwind
```

### Trabajar normal:
```sh
npm install
npm run dev
git add .
git commit -m "feat: nueva funcionalidad"
git push
```
### ⚠️ Esto commitea SOLO en el repo de la app.

---
## 🔄 Actualizar el repo padre después de cambios

### Volver al root del repo:
```sh
cd ..
git status
```
### Vas a ver algo como:
```txt
modified: chat-tailwind (new commits)
```
### Entonces
```git
git add chat-tailwind
git commit -m "update chat-tailwind submodule"
git push
```
### 📌 El repo padre guarda el nuevo hash del submodule.

---

## 🧹 Cómo eliminar un submodule correctamente
```sh
git submodule deinit -f nombre-app
rm -rf .git/modules/nombre-app
rm -rf nombre-app
```
### Editar .gitmodules y borrar la entrada correspondiente.
### Luego:
```git
git add .gitmodules
git commit -m "remove nombre-app submodule"
git push
```

---

## 🧠 Reglas de Oro (LEER SIEMPRE)

- ✅ El código se edita DENTRO del submodule
- ✅ El padre solo guarda commits, no código
- ✅ Siempre commitear:
    -   primero el submodule
    -   después el repo padre

- ❌ Nunca copiar archivos desde el repo padre
- ❌ Nunca hacer git add de archivos del submodule desde el padre
- ❌ No crear la carpeta antes de git submodule add


---

## 🧠 Filosofía del repo

### Este repositorio:
    - organiza múltiples apps Vue
    - mantiene independencia entre proyectos


## 🧪 Comandos útiles
```git
git submodule status
git submodule sync
git submodule update --init --recursive
```