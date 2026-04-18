# Axet CLI

Proxy inteligente para APIs de AI con autenticación y tracking de uso. Soporta OpenAI y AWS Bedrock.

## Instalación Rápida

### Linux / Mac

```bash
curl -fsSL https://raw.githubusercontent.com/codefensory/axet/main/install.sh | bash
```

### Windows

Requiere Git Bash o WSL:
```bash
curl -fsSL https://raw.githubusercontent.com/codefensory/axet/main/install.sh | bash
```

## Requisitos

- **Node.js 18+** ([Descargar](https://nodejs.org))
- Cuenta en Axet (para autenticación Okta)

## Comandos

| Comando | Descripción |
|---------|-------------|
| `axet login` | Autenticarse con Okta |
| `axet logout` | Cerrar sesión |
| `axet switch` | Cambiar de proyecto |
| `axet start` | Iniciar proxy server (default) |
| `axet update` | Actualizar el CLI |
| `axet --version` | Ver versión |
| `axet --help` | Mostrar ayuda |

## Uso Rápido

```bash
# 1. Iniciar sesión (solo la primera vez)
axet login

# 2. Iniciar el proxy server
axet start

# 3. Usar OpenAI apuntando a localhost
export OPENAI_BASE_URL=http://localhost:3001/v1
```

## Configuración

Crea un archivo `.env` en tu directorio de trabajo:

```env
PORT=3001                    # Puerto del proxy
AXET_API_URL=https://api.axet.ai
VERBOSE=false                # Logging detallado
```

## Auto-actualización

El CLI verifica automáticamente si hay nuevas versiones al iniciar el servidor.

Para actualizar manualmente:
```bash
axet update
```

Para reinstalar desde cero:
```bash
curl -fsSL https://raw.githubusercontent.com/codefensory/axet/main/install.sh | bash
```

## Estructura del Proyecto

```
~/.axet/                          # Código del CLI (instalado automáticamente)
├── index.production.js          # Entry point
├── dist/
│   └── axet.js                  # Código compilado
├── node_modules/                # Dependencias
└── package.json

~/.config/axet/                   # Configuración de usuario
└── state.json                    # Tokens y proyecto seleccionado

~/.local/share/axet/              # Datos de uso
└── usage-rxdb.json               # Tracking de uso
```

## Desinstalación

```bash
rm -rf ~/.axet ~/.local/bin/axet ~/.config/axet ~/.local/share/axet
```

## Troubleshooting

### "axet: command not found"

El directorio `~/.local/bin` no está en tu PATH. Agrega esto a tu `~/.bashrc` o `~/.zshrc`:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Luego recarga: `source ~/.bashrc` (o `~/.zshrc`)

### Error de permisos

Asegúrate de que el directorio `~/.local/bin` existe:
```bash
mkdir -p ~/.local/bin
```

### No detecta actualizaciones

El auto-updater requiere que existan **Releases** en GitHub. Si acabas de instalar y no detecta updates, espera a que el mantenedor publique una nueva versión.

## Licencia

MIT © codefensory
