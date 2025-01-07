name: github-actions-my-profile.yml

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  generate_cards:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'

      - name: Install profile-summary-card-generator
        run: |
          npm install -g profile-summary-card-generator

      - name: Generate profile cards
        run: |
          generate-profile-summary-cards -t solarized -u https://github.com/emiche1108

      - name: Upload generated cards to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages
          folder: ./profile-summary-card-output
