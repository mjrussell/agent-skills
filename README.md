# agent-skills

A collection of agent skills for AI assistants, providing CLI tools for various services.

## Available Skills

| Skill | Description | npm Package |
|-------|-------------|-------------|
| [anylist](./anylist/) | Manage grocery and shopping lists | [`anylist-cli`](https://www.npmjs.com/package/anylist-cli) |
| [hevy](./hevy/) | Query workout data from Hevy | [`hevy-cli`](https://www.npmjs.com/package/hevy-cli) |
| [paprika](./paprika/) | Access Paprika Recipe Manager | [`paprika-recipe-cli`](https://www.npmjs.com/package/paprika-recipe-cli) |
| [todoist](./todoist/) | Manage tasks with Todoist | [`todoist-ts-cli`](https://www.npmjs.com/package/todoist-ts-cli) |
| [trimet](./trimet/) | Portland transit data | [`trimet-cli`](https://www.npmjs.com/package/trimet-cli) |

## Installation

### Via clawdhub

```bash
npx clawdhub install anylist
npx clawdhub install hevy
# etc.
```

### Via npm (CLIs only)

```bash
npm install -g anylist-cli hevy-cli paprika-recipe-cli todoist-ts-cli trimet-cli
```

## About

These skills are designed to be used by AI assistants (like Claude) to interact with various services on behalf of users. Each skill includes:

- A `SKILL.md` file describing when and how to use the tool
- Reference to the underlying CLI tool (installed via npm)
- Usage examples for common scenarios

## Disclaimer

These are unofficial tools created by the community. They are not affiliated with, endorsed by, or connected to any of the services they interact with.

## License

MIT © [Matt Russell](https://github.com/mjrussell)
