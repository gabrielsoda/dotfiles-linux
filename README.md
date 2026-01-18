# dotfiles-linux

Configuración de terminal y herramientas CLI para Ubuntu Linux, gestionada con GNU Stow.

## Contenido

```
dotfiles/
├── zsh/
│   └── .zshrc           # Configuración de Zsh con Oh My Zsh, plugins y aliases
├── micro/
│   └── .config/
│       └── micro/
│           └── settings.json   # Configuración del editor micro
└── README.md
```

## Qué incluye

### Shell
- **Zsh** con **Oh My Zsh** como framework
- **Plugins**: autosuggestions, syntax-highlighting, z, extract, docker, docker-compose
- Aliases (`reload`, `zshconfig`, `ll`)
- Integración con fzf (keybindings)

### Herramientas CLI
- **fzf** — búsqueda fuzzy interactiva
- **ripgrep** — búsqueda rápida en archivos
- **bat** — cat con syntax highlighting
- **eza** — ls moderno con colores
- **tldr** — man pages simplificadas
- **micro** — editor de texto en terminal con atajos convencionales

## Restauración

### 1. Instalar dependencias

```bash
# Zsh y utilidades
sudo apt update
sudo apt install -y zsh stow git curl fzf ripgrep bat micro

# tldr y eza via snap
sudo snap install tldr
sudo snap install eza
```

### 2. Instalar Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 3. Instalar plugins de Zsh

```bash
# Autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Syntax highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### 4. Clonar este repositorio

```bash
git clone git@github.com:gabrielsoda/dotfiles-linux.git ~/dotfiles
```

### 5. Eliminar archivos existentes que serán reemplazados

```bash
# Backup opcional
mv ~/.zshrc ~/.zshrc.backup

# O eliminar directamente si no lo necesitás
rm ~/.zshrc
```

### 6. Aplicar configuración con Stow

```bash
cd ~/dotfiles
stow zsh
stow micro  # si existe el paquete
```

### 7. Recargar shell

```bash
source ~/.zshrc
```

## Verificación

```bash
# Verificar que .zshrc es un symlink
ls -la ~/.zshrc
# Debería mostrar: .zshrc -> dotfiles/zsh/.zshrc

# Probar herramientas
fzf --version
rg --version
bat --version
eza --version
micro --version
```

## Uso diario

### Atajos de teclado (fzf)

| Atajo | Función |
|-------|---------|
| `Ctrl+R` | Búsqueda interactiva en historial |
| `Ctrl+T` | Búsqueda de archivos |
| `Alt+C` | Cambio de directorio interactivo |

### Aliases incluidos

| Alias | Comando |
|-------|---------|
| `reload` | `source ~/.zshrc` |
| `zshconfig` | `micro ~/.zshrc` |
| `ll` | `ls -lah` |

### z

```bash
# Después de visitar directorios varias veces, podés saltar con:
z proyecto
z docker
z backend
```

## Agregar nueva configuración

```bash
# Ejemplo: agregar configuración de git
mkdir -p ~/dotfiles/git
mv ~/.gitconfig ~/dotfiles/git/
cd ~/dotfiles
stow git
git add .
git commit -m "Add git configuration"
git push
```

## Restaurar en caso de problemas

```bash
cd ~/dotfiles
stow -D zsh  # Elimina los symlinks
# Restaurar backup si existe
mv ~/.zshrc.backup ~/.zshrc
```
