# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

If the user's prompt starts with “EP:” or "ep:", then the user wants to enhance the prompt. Read the PROMPT_ENHANCER.md file and follow the guidelines to enhance the user's prompt. Show the user the enhancement and get their permission to run it before taking action on the enhanced prompt.

The enhanced prompts will follow the language of the original prompt (e.g., Korean prompt input will output Korean prompt enhancements, English prompt input will output English prompt enhancements, etc.)


### Development
```bash
npm start          # Start development server on http://localhost:3000
npm test           # Run tests with Jest in watch mode
npm run build      # Create production build in ./build directory
npm run deploy     # Build and deploy to GitHub Pages
```

### Testing
```bash
npm test                    # Run all tests in watch mode
npm test -- --coverage      # Run tests with coverage report
npm test SomeComponent      # Run tests matching pattern
npm test -- --watchAll=false # Run tests once without watch mode
```

## Architecture

### Routing Structure
The app uses React Router v7 with lazy loading for all routes. Key points:
- Base path is `/web` (configured for GitHub Pages deployment)
- All routes are lazy-loaded for optimal bundle size
- Routes are defined in `src/router/router.tsx`
- Sub-routes use `SubContentsTemplate` layout wrapper

### Component Organization
```
src/
├── pages/          # Route components (lazy loaded)
├── components/
│   ├── layout/     # Page structure (Header, Footer, etc.)
│   ├── sections/   # Reusable page sections
│   ├── lab/        # Lab/project specific components
│   └── ui/         # Shared UI components
```

### Active Feature Development
The DeductionGame feature (`src/components/lab/subject/DeductionGame/`) uses:
- Strategy pattern for AI difficulty levels
- Factory pattern for player creation
- TypeScript interfaces for type safety
- Separate concerns: GameManager, Players, Strategies

### Styling Approach
- Component-specific CSS files (e.g., `Component.css`)
- GSAP for animations
- React Intersection Observer for scroll-triggered effects

### TypeScript Configuration
- Strict mode enabled
- React JSX transform (no React import needed)
- Target: ES5 for browser compatibility

### Deployment
- GitHub Pages deployment via `gh-pages` package
- SPA routing handled in `public/index.html`
- Homepage: https://asyncsite.github.io/web



---



## Coding Principles and Design Guidelines

The code in this repository aims for the highest standards of readability, maintainability, and scalability. The following principles and guidelines should be followed to ensure a consistent and high-quality codebase.

### General Readability Principles

* **Clear Naming**: Use clear and descriptive names for variables, functions, and components. Avoid abbreviations and use names that provide context and reveal intent.
* **Single Responsibility Principle (SRP)**: Keep functions and components concise and focused on a single responsibility. If a component or function handles multiple tasks, actively consider refactoring it into smaller, more specialized units.
* **File Length and Refactoring** 📏: As a practical extension of SRP, pay close attention to file length.
  * If a file exceeds **1,000 lines**, it should be reviewed as a strong indicator that it has multiple responsibilities and should be considered for refactoring.
  * If a file exceeds **1,500 lines**, its refactoring **must be treated as a top-priority task**.
* **Consistent Style**: Maintain a consistent coding style and formatting across the entire project. This helps other developers read and understand the code more easily.
* **Purposeful Comments**: Code should be as self-documenting as possible. However, add clear comments to explain complex business logic or the reasoning behind specific implementation choices (the "why," not just the "what").


### Object-Oriented and Component-Based Design

While not every language or project requires a strict object-oriented paradigm, the following design principles are to be actively applied when working with these specific technologies to ensure high-quality, reusable, and maintainable code:
* **TypeScript**
* **React**
* **Java**
* **Kotlin**
* **Spring Framework**

#### Core Principles

* **Separation of Concerns (SoC)**
  Clearly separate concerns, such as logic, data, and presentation. For example, business logic should reside in service layers, data structures in models or DTOs, and user interface representation in components. This ensures that each part can be modified and tested independently.

* **Favor Composition over Inheritance**
  While inheritance is a powerful tool, it can lead to tight coupling. To build flexible and reusable structures, prioritize composition—combining objects with desired functionality—over extending them through inheritance. This is an especially critical principle in component-based frameworks like React.

* **Design by Contract with Interfaces**
  Define clear "contracts" between objects using TypeScript's `interface` or the `interface`/`abstract class` features in Java and Kotlin. This practice hides implementation details (encapsulation) and exposes a clear specification of an object's capabilities, leading to more predictable and stable code.

* **Use of Appropriate Design Patterns**
  We encourage the application of well-known design patterns (e.g., Factory, Strategy, Observer, Singleton) where they fit the problem. Using appropriate patterns provides structural consistency, reduces communication overhead among team members, and leads to more predictable and robust architectures.




## Architecture and Code Organization

A well-defined architecture is crucial for building scalable and maintainable applications. All code must be organized into logical layers and features, avoiding the practice of placing all functionality into a single file (e.g., a single large component or service class).

### Backend (Java, Kotlin, Spring)

Backend development **must follow the principles of Clean Architecture**. While more specific rules will be documented separately, the core mandate is to structure the application into distinct, independent layers.

* **Layered Structure**: The code must be separated into layers such as **Domain** (core business logic and entities), **Application** (use cases), and **Infrastructure** (frameworks, databases, external APIs).
* **Dependency Rule**: Inner layers (Domain) must not have any knowledge of or dependencies on outer layers (Infrastructure). Dependencies must only point inwards.
* **Separation**: All business logic cannot be concentrated in a single Controller or Service. Functionality must be properly distributed across use cases, domain services, and entities as appropriate.

### Frontend (TypeScript, React)

Frontend development **must follow a scalable, feature-based architecture** to ensure clear separation of concerns and reusability. The goal is to avoid creating massive "god components" that handle excessive state, logic, and rendering.

* **Component Structure**: Adhere to the established component organization (e.g., `pages`, `components/ui`, `components/sections`). More importantly, group components, hooks, and related logic by feature or domain wherever possible.
* **Logic and View Separation**:
    * **UI Components (Dumb Components)**: Should be primarily responsible for rendering and presentation.
    * **Container Logic (Smart Components/Hooks)**: Custom hooks or container components should be used to manage state, data fetching, and business logic, passing the necessary data and functions down to UI components as props.
* **API/Service Abstraction**: API calls and other external service interactions must be abstracted into dedicated modules or service files. They should not be embedded directly within components' rendering logic.