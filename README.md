# Screenmatch <a name="readme-top"></a>
![Static Badge](https://img.shields.io/badge/status-completed-green?style=for-the-badge)

## Introduction
**Screenmatch** is a Java-based application designed as an online movie platform. This project was developed to practice core Java concepts such as object-oriented programming (OOP), data collections, HTTP API consumption, and exception handling. Through this application, users can explore movies, manage a list of favorite films, and store them in files. The project also emphasizes modular design, encapsulation, and leveraging external APIs like OMDb.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Technologies](#technologies)
- [Contributors](#contributors)

## Installation

### Prerequisites
- Java JDK 18+ installed
- An IDE such as IntelliJ IDEA, Eclipse, or NetBeans installed

### Steps to run
1. Clone the repository:
   ```bash
   git clone https://github.com/victorhubarb/screenmatch.git
   cd screenmatch
   ```
2. Open the project in your preferred IDE:
- Import the project into your IDE (e.g., using “Open Project” in IntelliJ or “Import Project” in Eclipse).
- Ensure the project uses the correct Java SDK (JDK 18+).

3. Run the application:
- Locate the Main class in the project structure.
- Right-click on the Main class and select Run.

## Usage
The application allows users to explore and manage a list of favorite movies through API integration and user input. Users can search for movies using the OMDb API, manage their lists, and save their favorite films to a file.

## Features
- **Movie Management**:
  - Search for movies using the OMDb API.
  - Add movies to a favorites list.
  - Sort movies based on specific attributes.
- **Encapsulation and OOP**:
  - Classes are modeled to encapsulate attributes, ensuring controlled access.
  - Polymorphism is implemented to adapt methods based on subclasses.
- **Collections and Data Management**:
  - Use of ArrayList for managing movies.
  - Custom ordering and sorting of movies.
- **HTTP API Consumption**:
  - Integration with the OMDb API to fetch movie data.
  - Serialization and deserialization of JSON using the GSON library.
- **Exception Handling**:
  - Custom exceptions for error scenarios.
  - Graceful error handling for API calls and file operations.
- **File Management**:
  - Save and read favorite movie lists in a structured file format.

## Technologies
- **Java**
- **OMDb API**
- **GSON** (for JSON handling)
- **Java Collections Framework**
- **Java.net.http** (for API requests)

## Contributors
- [Victor Barbosa](https://github.com/victorhubarb)
<p align="right">(<a href="#readme-top">back to top</a>)</p>
