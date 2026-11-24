---
name: glua-agent-skill
description: Write and edit Lua code for Garry's Mod projects. Use when a task creates, changes, or reviews GLua code; preserve the project's existing conventions when editing established code.
---

# Garry's Mod Lua

Implement and maintain Lua code for Garry's Mod (GMod). Follow the user's request and the project's architecture. Respond in the language the user uses.

## Working with a project

- When the user asks to implement or change a feature, inspect the project and make the change in the relevant files. Return a standalone code example only when the user asks for one or no project files are available.
- Inspect relevant files and nearby code before editing. Follow project-specific APIs, naming, structure, and conventions when they are clear.
- For new code, use the Code Style below.
- When editing existing code, preserve the style of the surrounding code. Do not reformat unrelated code. Apply this skill's style to new code added in the same change unless doing so would make the result inconsistent or the user asks otherwise.
- Do not guess GMod, framework, or addon APIs. Check the project for established usage. Ask only when a missing detail blocks a safe implementation. Otherwise, make a conservative assumption, implement the feature, and state the assumption briefly.
- Do not add comments that merely restate the code or mention AI. Comment only non-obvious behavior. Document public APIs intended for other systems.
- Do not use an em dash. Use a hyphen instead.
- Do not create Markdown handoff files unless the user first agrees that one is needed.

## Code Style

### Formatting

- Use tabs for indentation, with an indent width of 3. Use UTF-8, remove trailing whitespace, and end files with a newline.
- Use standard Lua operators: `and`, `or`, `not`, and `~=`. Do not use GLua-only operator forms such as `&&`, `||`, `!`, or `!=`. `continue` is allowed.
- Use single-quoted strings by default. Escape an apostrophe inside one as `\\'`.
- Do not wrap conditions in unnecessary parentheses: `if coolDev then`.
- Keep lines to 120 characters where practical. For long expressions, break at logical groups and place `and` or `or` at the end of the continued line.
- In a multiline table, include a trailing comma after the final item.

### Naming and structure

- Use `camelCase` for variables and functions.
- Use `PascalCase` for metatables and their methods, for example `Item` and `Item:GetName()`.
- Use `ALL_CAPS` for enum-like constants stored in the module table, for example `myShop.ORDER_PLACED`.
- Name intentionally unused variables `_`.
- Put hooks and network message identifiers in the `module.submodule.name` form, for example `carDealer.carAdded` or `orgs.users.setRank`.
- Avoid unnecessary globals. Keep module state on a module table (for example `myShop = myShop or {}`); keep implementation details `local`.
- Use global module tables with dot functions for libraries and function collections. Use metatables, `:` methods, and `self` when shared instance behavior or another concrete need calls for them.

### Efficiency

- Keep static tables and values outside functions when that is appropriate. Cache computed values only when their validity can be maintained safely.
- Append to arrays with `t[#t + 1] = value` instead of `table.insert`.

### Comments and API documentation

- Prefer clear names over comments. Explain only logic whose purpose or constraints are not apparent from the code.
- Document public APIs used by other systems with this format:

```lua
--[[
	Description
	@param {type} name Description
	@param? {type} name Optional parameter description
	@returns {type} Description
]]
```

- A short comment is enough for a simple or unfinished function, for example `-- (bool) Checks whether ...`.
