# Text-Based System Bot

## Virtual Order Agent

A fast-food virtual ordering system being developed with **PostgreSQL, Docker, Kestra, Python, and Telegram**.

The goal of the project is to build a text-based virtual ordering agent where customers can interact with a fast-food business through a **Telegram bot**.

The system is being developed incrementally, starting with the database and workflow infrastructure and then adding the Telegram customer interface and ordering functionality.

---

## What the Project Does

The project is being developed as a virtual ordering system for a fast-food business.

The final system is designed to allow customers to:

* Start a conversation with the ordering assistant
* View the menu
* Ask about menu items
* Select food and drinks
* Specify quantities
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
                 │       Python        │
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