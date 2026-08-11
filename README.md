# Text-Based System Bot

## Virtual Order Agent

A fast-food virtual ordering system being developed with **PostgreSQL, Docker, Kestra, and Telegram**.

The goal of the project is to build a text-based virtual ordering agent where customers can eventually interact with the system through a **Telegram bot**.

Currently, the project includes the PostgreSQL database, Docker environment, and a Kestra workflow for retrieving menu items.

---

## What the Project Does

The project is being developed as a virtual ordering system for a fast-food business.

The system is designed to eventually allow customers to:

* View the menu
* Ask about menu items
* Select food and drinks
* Create an order
* Review their order
* Confirm their order

The planned customer-facing interface is a **Telegram bot**.

---

## System Architecture

The planned system will work approximately as follows:

```text
                         CUSTOMER
                            │
                            │ Telegram
                            ▼
                 ┌─────────────────────┐
                 │    TELEGRAM BOT     │
                 │  Customer Interface │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │  VIRTUAL ORDER      │
                 │      AGENT          │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │       KESTRA        │
                 │ Workflow Automation │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     POSTGRESQL      │
                 │                     │
                 │   ┌─────────────┐   │
                 │   │  menu_items │   │
                 │   └─────────────┘   │
                 │                     │
                 │   ┌─────────────┐   │
                 │   │    orders   │   │
                 │   └─────────────┘   │
                 └─────────────────────┘
```

> **Current status:** PostgreSQL, Docker, and the Kestra menu workflow are implemented. The Telegram bot, ordering agent, and order functionality are planned next.

---

## Project Structure

```text
text-based-system-bot/
├── database/
├── kestra/
│   └── fastfood_menu.yml
├── .env.example
├── .gitignore
├── README.md
├── docker-compose.yml
└── touch
```

---

## PostgreSQL Setup

PostgreSQL is used as the database for the fast-food system.

The database currently contains a `menu_items` table with information such as:

* `id`
* `name`
* `description`
* `price`
* `available`

The database provides the menu data used by the Kestra workflow.

PostgreSQL is run through Docker as part of the development environment.

---

## Docker

Docker is used to run the project's services in containers.

The services are configured in:

```text
docker-compose.yml
```

### Start the project

From the project directory, run:

```bash
docker compose up -d
```

Check the running containers:

```bash
docker compose ps
```

To stop the services:

```bash
docker compose down
```

Local PostgreSQL database data is excluded from Git using `.gitignore`.

---

## Kestra

Kestra is used for workflow orchestration.

The current Kestra workflow connects to PostgreSQL and retrieves menu items from the database.

The flow is stored in:

```text
kestra/fastfood_menu.yml
```

---

## `fastfood_menu` Flow

The current workflow is called:

```text
fastfood_menu
```

and belongs to the:

```text
fastfood
```

namespace.

The main task is:

```text
get_menu
```

It connects to PostgreSQL and executes:

```sql
SELECT
  id,
  name,
  description,
  price,
  available
FROM menu_items
ORDER BY id;
```

The purpose of this workflow is to retrieve the menu items from PostgreSQL.

The flow has been successfully executed in Kestra.

---

## How to Start the Project

### 1. Clone the repository

```bash
git clone https://github.com/holydopeengine/text-based-system-bot.git
cd text-based-system-bot
```

### 2. Configure environment variables

Copy the example environment file:

```bash
cp .env.example .env
```

Update `.env` with the required local configuration.

Do not commit `.env` to Git.

### 3. Start Docker services

```bash
docker compose up -d
```

Check that the services are running:

```bash
docker compose ps
```

---

## How to Run the Kestra Flow

1. Open the Kestra interface.
2. Open the `fastfood` namespace.
3. Open the `fastfood_menu` flow.
4. Execute the flow.
5. Open the new execution.
6. Check the `get_menu` task.
7. Check the logs and outputs.

A successful execution confirms that Kestra can connect to PostgreSQL and execute the menu query.

---

## Telegram Bot

The planned customer-facing interface is a **Telegram bot**.

Customers will eventually interact with the virtual ordering agent through Telegram.

The bot is intended to allow customers to:

* Start a conversation
* View the menu
* Select menu items
* Specify quantities
* Review an order
* Confirm an order

The Telegram bot has **not been implemented yet**.

---

## Current Progress

* [x] Initialize project
* [x] Set up PostgreSQL
* [x] Create menu database structure
* [x] Configure Docker
* [x] Configure `.gitignore`
* [x] Set up Kestra
* [x] Connect Kestra to PostgreSQL
* [x] Create `fastfood_menu` workflow
* [x] Successfully execute the menu query
* [ ] Build Telegram customer bot
* [ ] Connect Telegram bot to the ordering system
* [ ] Implement customer ordering
* [ ] Store customer orders
* [ ] Complete the virtual ordering workflow

---

## Next Steps

The next stage of development is to build the **Telegram customer bot** and connect it to the existing ordering system.

The final goal is a complete text-based fast-food ordering experience where customers can interact with the system through Telegram.
