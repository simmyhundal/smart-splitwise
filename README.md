# smart-splitwise

**EN** | [FR](#fr)

A GenAI-powered group expense tracker — a personal replacement for Splitwise built on n8n + Claude. Chat with the bot on Slack (WhatsApp coming soon) to add expenses, check balances, and settle up. All data lives in a Google Sheet.

## How it works

```
Slack / WhatsApp / Chat
        ↓
  Intent Router
  ├── "balance?" → reads Balances tab directly (no LLM, ~2s)
  └── everything else → Claude Sonnet (AI Agent)
                              ↓
              read / append / update Google Sheet
                              ↓
                      reply to user
```

## Workflows

| Workflow | Role |
|---|---|
| `expense-tracker-slack-bot` | Main bot — receives messages, routes intent, calls tools |
| `expense-tracker-read-expenses` | Tool: reads all rows from Expenses tab |
| `expense-tracker-read-balances` | Tool: reads pre-computed balances |
| `expense-tracker-append-expense` | Tool: appends a new expense row |
| `expense-tracker-update-expense` | Tool: updates an existing row by ID |

## Requirements

- [n8n](https://n8n.io) (self-hosted, tested on v2.57)
- Anthropic API key (Claude Sonnet)
- Google Sheets OAuth2 credential
- Slack app with `chat:write`, `im:history`, `channels:history` scopes
- Cloudflare Tunnel (or equivalent) to expose n8n publicly

## Setup

1. Import the JSON files in `workflows/` into n8n
2. Configure credentials: Anthropic, Google Sheets, Slack
3. Set the Google Sheet ID in each sub-workflow node
4. Start Cloudflare Tunnel: `cloudflared tunnel run n8n`
5. Set Slack Event Subscriptions URL: `https://n8n.mypart.llc/webhook/slack-events`
6. Subscribe to `message.im` and `message.channels`

## Google Sheet structure

Three tabs: **Instructions** · **Expenses** · **Balances**

The Expenses tab tracks every expense (description, amount, who paid, split). The Balances tab auto-computes who owes what.

---

<a name="fr"></a>

# smart-splitwise — FR

Un suivi de dépenses de groupe propulsé par GenAI — remplacement personnel de Splitwise, construit sur n8n + Claude. Chattez avec le bot sur Slack (WhatsApp bientôt) pour ajouter des dépenses, vérifier les bilans et régler les comptes. Toutes les données sont dans un Google Sheet.

## Comment ça marche

```
Slack / WhatsApp / Chat
        ↓
  Intent Router
  ├── "balance?" → lit l'onglet Balances directement (sans LLM, ~2s)
  └── tout le reste → Claude Sonnet (AI Agent)
                              ↓
            lire / ajouter / modifier Google Sheet
                              ↓
                    répondre à l'utilisateur
```

## Workflows

| Workflow | Rôle |
|---|---|
| `expense-tracker-slack-bot` | Bot principal — reçoit les messages, route les intentions, appelle les outils |
| `expense-tracker-read-expenses` | Outil : lit toutes les lignes de l'onglet Expenses |
| `expense-tracker-read-balances` | Outil : lit les bilans pré-calculés |
| `expense-tracker-append-expense` | Outil : ajoute une nouvelle ligne de dépense |
| `expense-tracker-update-expense` | Outil : met à jour une ligne existante par ID |

## Prérequis

- [n8n](https://n8n.io) (auto-hébergé, testé sur v2.57)
- Clé API Anthropic (Claude Sonnet)
- Credential Google Sheets OAuth2
- App Slack avec les scopes `chat:write`, `im:history`, `channels:history`
- Cloudflare Tunnel (ou équivalent) pour exposer n8n publiquement

## Installation

1. Importer les fichiers JSON de `workflows/` dans n8n
2. Configurer les credentials : Anthropic, Google Sheets, Slack
3. Définir l'ID du Google Sheet dans chaque nœud sub-workflow
4. Lancer Cloudflare Tunnel : `cloudflared tunnel run n8n`
5. Configurer l'URL Event Subscriptions Slack : `https://n8n.mypart.llc/webhook/slack-events`
6. S'abonner aux événements `message.im` et `message.channels`

## Structure du Google Sheet

Trois onglets : **Instructions** · **Expenses** · **Balances**

L'onglet Expenses enregistre chaque dépense (description, montant, qui a payé, répartition). L'onglet Balances calcule automatiquement qui doit quoi.
