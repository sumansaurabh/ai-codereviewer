# Revisor de Código con IA

Revisor de Código con IA es una GitHub Action que aprovecha la API GPT-4 de OpenAI para proporcionar comentarios inteligentes y sugerencias sobre tus pull requests. Esta poderosa herramienta ayuda a mejorar la calidad del código y ahorra tiempo a los desarrolladores al automatizar el proceso de revisión de código.

## Características

- Revisa pull requests utilizando la API GPT-4 de OpenAI.
- Proporciona comentarios inteligentes y sugerencias para mejorar tu código.
- Filtra archivos que coinciden con patrones de exclusión especificados.
- Fácil de configurar e integrar en tu flujo de trabajo de GitHub.

## Configuración

1. Para usar esta GitHub Action, necesitas una clave API de OpenAI. Si no tienes una, regístrate para obtener una clave API
   en [OpenAI](https://beta.openai.com/signup).

2. Agrega la clave API de OpenAI como un GitHub Secret en tu repositorio con el nombre `OPENAI_API_KEY`. Puedes encontrar más
   información sobre GitHub Secrets [aquí](https://docs.github.com/en/actions/reference/encrypted-secrets).

3. Crea un archivo `.github/workflows/main.yml` en tu repositorio y agrega el siguiente contenido:

```yaml
name: AI Code Reviewer

on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: AI Code Reviewer
        uses: your-username/ai-code-reviewer@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # El GITHUB_TOKEN está allí por defecto, así que solo necesitas mantenerlo como está y no es necesario agregarlo como secreto ya que arrojará un error. [Más Detalles](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # Opcional: por defecto es "gpt-4"
          exclude: "**/*.json, **/*.md" # Opcional: patrones de exclusión separados por comas
```

4. Reemplaza `your-username` con tu nombre de usuario de GitHub o nombre de organización donde se encuentra el repositorio de AI Code Reviewer.

5. Personaliza la entrada `exclude` si deseas ignorar ciertos patrones de archivos de la revisión.

6. Confirma los cambios en tu repositorio, y AI Code Reviewer comenzará a trabajar en tus futuros pull requests.

## Cómo Funciona

La GitHub Action AI Code Reviewer recupera el diff del pull request, filtra los archivos excluidos y envía fragmentos de código a la API de OpenAI. Luego genera comentarios de revisión basados en la respuesta de la IA y los agrega al pull request.

## Contribuciones

¡Las contribuciones son bienvenidas! No dudes en enviar issues o pull requests para mejorar la GitHub Action AI Code Reviewer.

Deja que el mantenedor genere el paquete final (`yarn build` & `yarn package`).

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más información.
