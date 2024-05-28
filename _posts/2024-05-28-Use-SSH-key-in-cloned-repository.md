---
title: "Use-SSH-Key-in-cloned-repository"
date: 2024-05-28
---


# Cómo usar la SSH key en un repositorio clonado.

## El problema

A veces se quiere utilizar la SSH key, pero sin querer se clona usando la URL del repositorio con protocolo HTTPS.

Esto hace que tengas que utilizar las credenciales de tu cuenta GitHub en lugar de tu key SSH.

## Intro

Cuando hacemos 
```
git clone REPO_URL
```
se descarga la branch principal del repositorio remoto a nuestra máquina.

Dependiendo del protocolo de la URL, Git va a utilizar para las operaciones de fetch/pull/push: 
- [ ] las credenciales de tu cuenta de GitHub (HTTPS).
- [ ] la SSH key (SSH)

Estos son los 2 posibles formatos de la URL de un repositorio:

- [ ] REPO_URL con protocolo HTTPS: https://github.com/NOMBRE_USUARIO/NOMBRE_REPO.git

- [ ] REPO_URL usando SSH key: git@github.com:NOMBRE_USUARIO/NOMBRE_REPO.git

## ¿Cómo solucionar esto? 

Simplemente debemos cambiar la REPO_URL del REMOTE, que por default es "origin".

### Paso 1

Checkear la URL del remote
```
git remote -v
```
Podrás verificar que la URL está usando protocolo HTTPS, ya que empieza con "https://".

### Paso 2

Copia o ten a mano el NOMBRE_USUARIO y NOMBRE_REPO.git de la URL. También comprueba el nombre del REMOTE, que en general será "origin".

### Paso 3

Cambiar URL del remote a SSH, usando NOMBRE_USUARIO y NOMBRE_REPO.git del paso anterior.
```
git remote set-url REMOTE_NAME git@github.com:NOMBRE_USUARIO/NOMBRE_REPO.git
```
Eso sería todo. Ahora Git te debería de pedir la SSH key en lugar de las credenciales al hacer fetch/pull/push.

# Referencias

https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#changing-a-remote-repositorys-url