# Instalación y configuración del software

## node

```
curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install build-essential
```

Comprobamos que esté instalado:

```
npm -v
node -v
```


## git

```
sudo apt-get update
sudo apt-get install git
```

- Mi configuración, necesaria para cada commit que haga:

git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"

- Opcionalmente el editor (si no me gusta el que hay por defecto):

git config --global core.editor vi

### configuración de git

- Git tiene 3 niveles de configuración, cada nivel sobreescribe el anterior:
    - Para todos los usuarios: */etc/gitconfig*
    - Para un usuario: *~/.gitconfig*  (opción --global)
    - Para un repositorio: *.git/config* 

- Para ver los parámetros configurados:

```
git config --list
```

### Configuración de GitHub
- Nos registramos en [Github](https://github.com/) 
- Accedemos a nuestra cuenta
- Vamos a los settings y asociamos una ssh-key
    - Evitaremos introducir usuario/contraseña en cada *git push*
- Como creamos nuestra ssh-key:

```
ssh-keygen
```
- Copiaremos el contenido de ~/.ssh/id_rsa.pub a una nueva clave ssh en GitHub

## Instalación de fish

- Algunos prefieren zsh
- Otros son fieles a bash
- ¿Por qué fish?
    - Gran experiencia de usuario "out of the box":
        - Sugiere comandos
        - Autocompleta
        - [Personalizaciones](https://github.com/justinmayer/tacklebox)

```
sudo apt-add-repository ppa:fish-shell/release-2
sudo apt-get update
sudo apt-get install fish
chsh -s `which fish`
```

### Instalación de Sublime Text 3

