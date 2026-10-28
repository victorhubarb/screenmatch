# Screenmatch

A Java console program that searches movies and series on the [OMDb API](https://www.omdbapi.com/), turns the response into its own `Titulo` model, and saves what you searched to `filmes.json`. Around it there is a small model of movies, series and episodes that practices inheritance, interfaces and collections.

## What's inside

There are three entry points in `main/`, going from simple to complete:

- **`Main`** builds movies, a series and an episode by hand. It rates them, adds up total runtime with `CalculadoraDeTempo`, and runs `FiltroRecomendacao` over anything that implements `Classificavel`.
- **`MainComListas`** works with `ArrayList` and `LinkedList`, sorts titles with `Comparable` and with `Comparator.comparing`, and uses pattern matching for `instanceof`.
- **`MainComBusca`** asks for a title in a loop, calls OMDb with `HttpClient`, maps the JSON into the `TituloOmdb` record with GSON, converts it to a `Titulo`, and writes the whole list to `filmes.json` when you type `sair`.

Design points:

- `Filme` and `Serie` extend `Titulo`. `Serie` overrides `getDuracaoEmMinutos()` to compute seasons × episodes × minutes.
- `Classificavel` is an interface implemented by `Filme` and `Episodio`, so the filter does not care which one it gets.
- `ErroDeConversaoDeAnoException` is a custom unchecked exception, thrown when OMDb returns a year such as `2010–2015` that cannot become an `int`.

The prompts and messages are in Portuguese.

## Run it

Requires JDK 17 or newer and the [GSON jar](https://mvnrepository.com/artifact/com.google.code.gson/gson). There is no build tool.

```bash
git clone https://github.com/victorhubarb/screenmatch.git
cd screenmatch
javac -cp gson-2.10.1.jar -d out $(find src -name "*.java")
java -cp "out:gson-2.10.1.jar" br.com.alura.screenmatch.main.MainComBusca   # ; instead of : on Windows
```

Swap `MainComBusca` for `Main` or `MainComListas` to run the other two; those need no network.

## Project structure

```
src/br/com/alura/screenmatch/
├── modelos/      Titulo, Filme, Serie, Episodio, TituloOmdb (record)
├── calculos/     Classificavel, CalculadoraDeTempo, FiltroRecomendacao
├── exception/    ErroDeConversaoDeAnoException
└── main/         Main, MainComListas, MainComBusca
filmes.json       Sample output from a search session
```

## Known gaps

- **The OMDb API key is hardcoded in `MainComBusca.java`** and is in the git history. It is a free key and should be revoked, and the next version will read it from an environment variable.
- A title that OMDb does not find comes back with null fields and the program fails on it, because only some parse errors are caught.
- Runtime is read as the first two characters of the OMDb string, so a 100-minute movie is stored as 10.
- The title is not URL-encoded beyond replacing spaces.
- No tests.

---

Victor Hugo Barbosa · [GitHub](https://github.com/victorhubarb) · [LinkedIn](https://www.linkedin.com/in/victorhbarbosa/)
