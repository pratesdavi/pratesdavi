# Olá, sou Davi Prates! 👋

Atuo na área de dados, acumulando experiência em análise, validação e tratamento de informações para assegurar que estejam sempre padronizadas, íntegras e consistentes. Integro a equipe de Business Intelligence (BI) de uma agência de trade marketing, contribuindo diretamente para a preparação de dados que sustentam decisões estratégicas e resultados relevantes.

Acredito que dados bem cuidados são como bons ingredientes em uma receita: quando a matéria-prima é de qualidade, o resultado final alcança todo o seu potencial. Por esse motivo, exerço um papel fundamental na cadeia de trabalho, pois o sucesso das análises e relatórios está diretamente ligado à confiabilidade e organização dos dados sob minha responsabilidade.

## 💡 Sobre meu trabalho

- Especialista em SQL para manipulação, extração e modelagem de dados em diferentes fontes.
- Experiência em ferramentas de análise e visualização de dados, como Excel, Power Query e Power BI (em constante aprendizado).
- Foco absoluto na padronização, validação e tratamento de dados para assegurar qualidade e confiança nas informações.
- Responsável por estruturar e organizar bancos de dados, otimizando processos internos e facilitando o acesso às informações para toda a equipe.

## 🛠️ Habilidades

- **SQL** (consultas, manipulação e modelagem de dados)
- **Power Query** (tratamento e transformação de dados)
- **Power BI** (visualização e dashboards – em desenvolvimento)
- **Excel** (apoio à análise de dados)
- **Python** (aprendendo)
- Validação e padronização de bases de dados

## 📫 Como me encontrar

- [LinkedIn](https://www.linkedin.com/in/davi-prates/)

---

> "Onde há dados de qualidade, há confiança nas decisões."  
> — Thomas C. Redman (“The Data Doc”)

----------

name: GitHub Snake Game

on:
  # Schedule the workflow to run daily at midnight UTC
  schedule:
    - cron: "0 0 * * *"
  # Allow manual triggering of the workflow
  workflow_dispatch:
  # Trigger the workflow on pushes to the main branch
  push:
    branches:
      - main
jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      # Step 1: Checkout the repository
      - name: Checkout Repository
        uses: actions/checkout@v3
      # Step 2: Generate the snake animations
      - name: Generate GitHub Contributions Snake Animations
        uses: Platane/snk@v3
        with:
          # GitHub username to generate the animation for
          github_user_name: ${{ github.repository_owner }}
          # Define the output files and their configurations
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/ocean.gif?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      # Step 3: Deploy the generated files to the 'output' branch
      - name: Deploy to Output Branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
          # Optionally, you can set a custom commit message
          commit_message: "Update snake animation [skip ci]"
