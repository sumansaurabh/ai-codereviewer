# Réviseur de Code IA

Réviseur de Code IA est une GitHub Action qui exploite l'API GPT-4 d'OpenAI pour fournir des commentaires intelligents et des suggestions sur vos pull requests. Cet outil puissant aide à améliorer la qualité du code et fait gagner du temps aux développeurs en automatisant le processus de révision de code.

## Fonctionnalités

- Révise les pull requests en utilisant l'API GPT-4 d'OpenAI.
- Fournit des commentaires intelligents et des suggestions pour améliorer votre code.
- Filtre les fichiers qui correspondent aux modèles d'exclusion spécifiés.
- Facile à configurer et à intégrer dans votre workflow GitHub.

## Configuration

1. Pour utiliser cette GitHub Action, vous avez besoin d'une clé API OpenAI. Si vous n'en avez pas, inscrivez-vous pour obtenir une clé API sur [OpenAI](https://beta.openai.com/signup).

2. Ajoutez la clé API OpenAI en tant que Secret GitHub dans votre dépôt avec le nom `OPENAI_API_KEY`. Vous pouvez trouver plus d'informations sur les Secrets GitHub [ici](https://docs.github.com/en/actions/reference/encrypted-secrets).

3. Créez un fichier `.github/workflows/main.yml` dans votre dépôt et ajoutez le contenu suivant :

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
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # Le GITHUB_TOKEN est présent par défaut, vous devez simplement le conserver tel quel et ne pas nécessairement l'ajouter en tant que secret car cela générera une erreur. [Plus de détails](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # Optionnel : par défaut "gpt-4"
          exclude: "**/*.json, **/*.md" # Optionnel : modèles d'exclusion séparés par des virgules
```

4. Remplacez `your-username` par votre nom d'utilisateur GitHub ou le nom de l'organisation où se trouve le dépôt AI Code Reviewer.

5. Personnalisez l'entrée `exclude` si vous souhaitez ignorer certains modèles de fichiers lors de la révision.

6. Validez les modifications dans votre dépôt, et AI Code Reviewer commencera à fonctionner sur vos futures pull requests.

## Comment ça fonctionne

La GitHub Action AI Code Reviewer récupère le diff de la pull request, filtre les fichiers exclus et envoie des morceaux de code à l'API OpenAI. Elle génère ensuite des commentaires de révision basés sur la réponse de l'IA et les ajoute à la pull request.

## Contribution

Les contributions sont les bienvenues ! N'hésitez pas à soumettre des issues ou des pull requests pour améliorer la GitHub Action AI Code Reviewer.

Laissez le mainteneur générer le package final (`yarn build` & `yarn package`).

## Licence

Ce projet est sous licence MIT. Consultez le fichier [LICENSE](LICENSE) pour plus d'informations.
