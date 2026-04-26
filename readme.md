# 🚀 Amethyst Project - 1 Page Cheat Sheet

## 1. 📝 Naming Conventions

> **Why?** To instantly identify variables, classes, and functions (internal vs external) just by their names, reducing communication overhead.

|Type|Rule|Example|
|:--|:--|:--|
|**Classes, Nodes, File Names**|`PascalCase`|`PlayerCharacter`, `HealthComponent.gd`|
|**Variables, Functions, Folders**|`snake_case`|`player_health`, `calculate_damage()`|
|**Private Variables/Functions**|`_` prefix|`_internal_counter` (prevents external access)|
|**Constants**|`UPPER_SNAKE_CASE`|`MAX_WAVE_COUNT`|
|**Signals**|Past (event) / Present (request)|`damage_taken`, `attack_requested`|

---

## 2. 🏗️ Architecture & Components

> **Why?** To ensure code doesn’t break when the scene structure changes and to maximize reusability across the project.

- **Unidirectional Dependency:** Higher-level systems (UI/Managers) can depend on lower-level systems, but lower-level systems (Domain/Core) must not depend on higher-level ones. Otherwise, UI changes can break core game logic.
    
- **Component Independence:** Components should not know “who” their parent is. This allows a `HealthComponent` to be reused across players, enemies, and destructible objects.
    
- **Avoid Direct Node Access (`@export` recommended):** Using `get_node("../../")` is fragile—moving a node can break everything at runtime. `@export` allows the editor to manage references safely.
    

---

## 3. 🔌 Dependencies & Type Safety

> **Why?** To maintain flexibility and improve testability. Direct dependency on singletons makes it hard to swap systems or use mock data.

- **Use Service Locator:** Avoid hardcoding singleton names like `Global.currency`. Access services through a layer:
    
    ```gdscript
    var currency = ServiceLocator.get_service("currency")
    ```
    
    This allows you to swap real systems with mock implementations with minimal changes.
    
- **Static Type Hints Required:** Adding types enables auto-completion and catches errors before runtime (compile-time safety).
    
    ```gdscript
    func take_damage(amount: float) -> void:
    ```
    

---

## 4. 📜 Script Layout

> **Why?** A consistent file structure reduces scanning time and makes it much easier to read others’ code.

1. `class_name` / `extends`
    
2. `signal` / `enum` / `const`
    
3. `@export` / `var`
    
4. Engine callbacks (`_ready`, `_process`)
    
5. Public methods → Private methods (`_`)
    
6. Signal handlers (`_on_...`)
    

---

## 5. 🌳 Git Workflow

> **Why?** To maintain a clean project history and make debugging easier.

- **Commit Prefixes:** Use `feat:`, `fix:`, `refactor:`, `docs:` to clearly indicate the nature of changes.
    
- **Principle:** Separate refactoring (structural changes) from feature additions. Mixing them makes debugging difficult.
    

---

**💡 For the Team:** These rules are not meant to restrict you—they exist to protect our **productivity** and **code quality** as the project grows.
