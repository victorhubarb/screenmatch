# Screenmatch 🎬

![Status](https://img.shields.io/badge/status-completed-green?style=for-the-badge)
![Java](https://img.shields.io/badge/Java-OOP%20%2B%20API-orange?style=for-the-badge&logo=java)

A Java application that consumes the OMDb API to search movies and tv shows, evaluate them, calculate total runtime, filter by rating, and save results to JSON — with a full OOP architecture, a custom exception, and an interface.

---

## Overview

Screenmatch was built to practice real-world Java beyond simple exercises. It connects to the OMDb API via `java.net.http.HttpClient`, deserializes JSON responses with GSON, and lets users search for titles, rate them, and save their favorites to a file. The class hierarchy models how a real streaming platform might organize content — `Titulo` as the base, with `Filme` and `Serie` extending it. A `Classificavel` interface enforces a rating contract, and `FiltroRecomendacao` uses it to categorize titles without knowing their concrete type.

The project has three separate entry points, each demonstrating a different stage of complexity.

---

## Architecture

```
br.com.alura.screenmatch/
├── modelos/
│   ├── Titulo.java                         # Base class — name, year, duration, ratings, Comparable
│   ├── Filme.java                          # Extends Titulo, implements Classificavel — adds director
│   ├── Serie.java                          # Extends Titulo — adds seasons, episodes, minutes per episode
│   ├── Episodio.java                       # Models individual episodes
│   └── TituloOmdb.java                     # Record — DTO for deserializing OMDb API responses
├── calculos/
│   ├── Classificavel.java                  # Interface — enforces getClassificacao() contract
│   ├── CalculadoraDeTempo.java             # Accumulates total runtime across a list of titles
│   └── FiltroRecomendacao.java             # Filters titles by rating using Classificavel interface
├── exception/
│   └── ErroDeConversaoDeAnoException.java  # Custom RuntimeException for year parsing errors
└── main/
    ├── Main.java                           # Basic entry point — manual title creation and evaluation
    ├── MainComListas.java                  # Collections entry point — sorting, filtering, ArrayList
    └── MainComBusca.java                   # Full entry point — OMDb API search + GSON + file save
```

### Key Concepts Applied

| Concept | How it shows up |
|---|---|
| **Inheritance** | `Filme` and `Serie` both extend `Titulo`; `Serie` overrides `getDuracaoEmMinutos()` to calculate from seasons × episodes × minutes |
| **Interface** | `Classificavel` enforces `getClassificacao()` — `Filme` implements it; `FiltroRecomendacao` uses it without knowing the concrete type |
| **Comparable** | `Titulo` implements `Comparable<Titulo>` — enables `Collections.sort()` by title name |
| **Custom Exception** | `ErroDeConversaoDeAnoException` is thrown when the OMDb year field has more than 4 characters |
| **HTTP API** | `HttpClient` + `HttpRequest` from `java.net.http` — no external library needed |
| **GSON** | `GsonBuilder` with `UPPER_CAMEL_CASE` naming policy deserializes OMDb JSON into `TituloOmdb` record |
| **Java Record** | `TituloOmdb` is a record — immutable DTO with concise syntax |
| **File I/O** | `MainComBusca` saves the search results list to `filmes.json` using `FileWriter` |
| **Collections** | `ArrayList<Titulo>` with `Collections.sort()`, stream filtering, and lambda expressions |

---

## How to Run

**Prerequisites:** Java 18+ · IntelliJ IDEA or Eclipse · GSON library on classpath · OMDb API key (free at [omdbapi.com](https://www.omdbapi.com/))

```bash
git clone https://github.com/victorhubarb/screenmatch.git
cd screenmatch
```

Open in your IDE and run one of the three Main classes:

- **`Main.java`** — creates titles manually and tests evaluation logic
- **`MainComListas.java`** — works with collections, sorting, and filtering
- **`MainComBusca.java`** — searches OMDb API, saves results to `filmes.json`

Add your OMDb API key in the URL string inside `MainComBusca.java` before running.

---

## What I'd Improve Next

- Move the API key to an environment variable — hardcoding it is a known limitation
- Add a proper CLI menu so the user can switch between modes without changing the entry point
- Expand `Serie` to fetch season/episode data from the OMDb API instead of hardcoded values

---

## Author

**Victor Hugo Barbosa**
[GitHub](https://github.com/victorhubarb) · [LinkedIn](https://www.linkedin.com/in/victorhbarbosa/)
