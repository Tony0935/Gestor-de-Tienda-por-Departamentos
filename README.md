# Gestor-de-Tienda-por-Departamentos

Java desktop application that manages department stores and their articles using manually implemented stack (LIFO) and queue (FIFO) structures — built from raw object arrays, without relying on any of Java's built-in collection classes.

## Overview

This is an academic Data Structures project (NetBeans, Java Swing). The core constraint was to implement stack and queue behavior **from scratch using object arrays**, with no use of `Stack`, `Queue`, `ArrayList`, or any other Java Collections API class.

- **Departments** are stored in a fixed-size array (20 elements) acting as a **stack** — last department added is the first one removed.
- Each department holds its own fixed-size array (20 elements) of **articles**, acting as an independent **queue** — first article added is the first one removed.
- Data persists in memory for the duration of the session (no database).

## Features

- **Department registration** — auto-generated unique ID, name; displayed in a live-updating table.
- **Article registration** — auto-generated unique ID (shared sequence across all departments), name, and category (predefined list: clothing, electronics, home, beauty, sports, toys, food/beverage); linked to a selected department's article queue.
- **Article removal** — removes the article at the front of the selected department's queue (the oldest one), matching FIFO semantics — no manual selection of which article to remove.
- **Article transfer** — moves an entire article queue from one department to another, with validation: at least 2 departments must exist, the source must have at least one article, and source/destination must differ.
- **Department removal** — removes the most recently added department (LIFO), and only if its article queue is empty; otherwise the operation is blocked with a message explaining why.

## Project Structure

Source: `src/main/java/Proyecto/gestortiendadepartamentos/`

| File | Responsibility |
|---|---|
| `GestorTienda.java` | Stack logic over a fixed-size `Departamento[]` array — push/pop-style add/remove, plus the transfer operation between departments |
| `Departamento.java` | Department entity, holding its own article queue — implemented as a **circular buffer** (front/rear indices with modulo arithmetic) rather than a naive array with element-shifting on removal |
| `Articulo.java` | Article entity (getters/setters) |
| `RegistroDepartamentosGUI.java` | Department registration screen |
| `RegistroArticulosGUI.java` | Article registration screen |
| `EliminacionArticulosGUI.java` | Article removal screen |
| `EliminacionDepartamentosGUI.java` | Department removal screen |
| `TrasladoArticulosGUI.java` | Article transfer between departments |
| `MenuPrincipalGUI.java` | Main menu / navigation |

**Implementation note:** the article queue in `Departamento` uses `frente`/`fin` indices with modulo wraparound (`(fin + 1) % max`) instead of shifting array elements on every dequeue — a proper circular queue rather than a simplified array-based approximation.

## Tech Stack

- **Language:** Java
- **UI:** Java Swing (NetBeans GUI forms)
- **Data Structures:** Manually implemented stack and queue using fixed-size object arrays (no Java Collections API)

## UI/UX Constraints

- Tables (`JTable`) for all list displays, refreshed after each operation.
- No `MessageBox`-style dialogs for routine input/output — only for validation errors (e.g., blocked department deletion, invalid transfer).

## Status

Completed academic project. Not under active development.

## Author

**Anthony Mendoza Rivas**
[LinkedIn](http://www.linkedin.com/in/anthonymendozarivas) · [GitHub](https://github.com/Tony0935)
