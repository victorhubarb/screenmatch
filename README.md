# Screenmatch 🎬

![Status](https://img.shields.io/badge/status-completed-green?style=for-the-badge)
![Java](https://img.shields.io/badge/Java-OOP%20%2B%20API-orange?style=for-the-badge&logo=java)

A Java application that consumes the OMDb API to search movies and series, evaluate them, calculate total runtime, filter by rating, and save results to a JSON file — with a full OOP architecture, a custom exception, and an interface.

---

## Overview

Most Java exercises stop at the console. This one goes further — it actually connects to the internet, talks to a real API, and saves data to disk. The idea was to build something closer to what real applications do: fetch data from OMDb, deserialize the JSON response with GSON, evaluate titles through a shared `Classificavel` interface, and let the user build a favorites list that persists between runs.

The project has three separate entry points, each showing a different layer of complexity — from manual object creation to full API integration with file persistence.

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
│   └── FiltroRecomendacao.java             # Filters titles by rating using Classificavel
├── exception/
│   └── ErroDeConversaoDeAnoException.java  # Custom RuntimeException for year parsing errors
└── main/
    ├── Main.java                           # Basic entry point — manual title creation
    ├── MainComListas.java                  # Collections — sorting, filtering, ArrayList
    └── MainComBusca.java                   # Full entry point — OMDb API + GSON + file save
```

### Key Concepts Applied

| Concept | How it shows up |
|---|---|
| **Inheritance** | `Filme` and `Serie` both extend `Titulo`; `Serie` overrides `getDuracaoEmMinutos()` |
| **Interface** | `Classificavel` enforces `getClassificacao()` — `FiltroRecomendacao` uses it without knowing the concrete type |
| **Comparable** | `Titulo` implements `Comparable<Titulo>` — enables `Collections.sort()` by title name |
| **Custom Exception** | `ErroDeConversaoDeAnoException` is thrown when the OMDb year field has more than 4 characters |
| **HTTP API** | `HttpClient` + `HttpRequest` from `java.net.http` |
| **GSON** | Deserializes OMDb JSON into `TituloOmdb` record using `GsonBuilder` |
| **Java Record** | `TituloOmdb` is a record — immutable DTO with concise syntax |
| **File I/O** | `MainComBusca` saves results to `filmes.json` using `FileWriter` |

---

## How to Run

**Prerequisites:** Java 18+ · IntelliJ IDEA or Eclipse · GSON on classpath · OMDb API key (free at [omdbapi.com](https://www.omdbapi.com/))

```bash
git clone https://github.com/victorhubarb/screenmatch.git
cd screenmatch
```

Open in your IDE and run one of the three Main classes. Add your OMDb API key in `MainComBusca.java` before running.

---

## What I'd Improve Next

- Move the API key to an environment variable — hardcoding it is a known limitation
- Add a proper CLI menu so the user can switch between modes at runtime
- Expand `Serie` to fetch season and episode data directly from the OMDb API

---

## Author

**Victor Hugo Barbosa**
[GitHub](https://github.com/victorhubarb) · [LinkedIn](https://www.linkedin.com/in/victorhbarbosa/)
