# ESLint Config Reference

Built on [`@antfu/eslint-config`](https://github.com/antfu/eslint-config).

## General Config

```ts
// eslint.config.mjs
import antfu from "@antfu/eslint-config";

export default antfu(
  {
    type: "app",
    formatters: true,
    typescript: { tsconfigPath: "./tsconfig.json" },
    stylistic: {
      quotes: "double",
      indent: 2,
      semi: true,
    },
    ignores: [
      "**/docs/*",
      "**/.next/*",
      "**/build/*",
      "**/shared/components/ui/*",
      "**/.husky/*",
    ],
  },
  {
    rules: {
      // pnpm settings
      "pnpm/yaml-enforce-settings": "off",

      // file style
      "object-curly-newline": ["error", { multiline: true, minProperties: 2 }],
      "style/function-paren-newline": ["error", { minItems: 2 }],
      "style/array-bracket-newline": ["error", { minItems: 2 }],
      "style/array-element-newline": ["error", { minItems: 2 }],
      "style/function-call-argument-newline": ["error", "always"],

      // typescript
      "perfectionist/sort-imports": "error",
      "ts/consistent-type-definitions": ["error", "type"],
      "ts/no-unsafe-assignment": "off",
      "ts/no-unsafe-call": "off",
      "ts/no-redeclare": "off",

      // general
      "no-console": "warn",
      "antfu/no-top-level-await": "off",
      "node/no-process-env": "error",

      // file naming
      "unicorn/filename-case": ["error", { case: "kebabCase", ignore: ["README.md"] }],

      // React rules
      "style/jsx-max-props-per-line": ["error", { maximum: 1 }],
    },
  },
);
```

### Type Reference

```ts
type AntfuConfig = {
  type: "app" | "lib";              // "app" disables some lib-only rules
  react: boolean;                    // enables React + hooks rules
  nextjs: boolean;                   // enables Next.js rules
  formatters: boolean;               // enables formatter rules (CSS, HTML, etc.)
  typescript: {
    tsconfigPath: string;            // path to tsconfig for type-aware rules
  };
  stylistic: {
    quotes: "double" | "single";
    indent: number;
    semi: boolean;
  };
  ignores: string[];                 // glob patterns to exclude from linting
};
```

## Rules

### pnpm

| Rule | Value | Why |
|------|-------|-----|
| `pnpm/yaml-enforce-settings` | `off` | prevents auto-fixing `trustPolicy` in `pnpm-workspace.yaml` |

### File Style

| Rule | Value | Why |
|------|-------|-----|
| `object-curly-newline` | `error` — multiline, min 2 props | forces multi-prop objects onto multiple lines |
| `style/function-paren-newline` | `error` — min 2 args | newline when function has 2+ args |
| `style/array-bracket-newline` | `error` — min 2 items | newline when array has 2+ items |
| `style/array-element-newline` | `error` — min 2 items | each element on its own line |
| `style/function-call-argument-newline` | `error` — always | every call argument on its own line |

### TypeScript

| Rule | Value | Why |
|------|-------|-----|
| `perfectionist/sort-imports` | `error` | enforces sorted import order |
| `ts/consistent-type-definitions` | `error` — `type` | prefer `type` over `interface` |
| `ts/no-unsafe-assignment` | `off` | relaxed for React component props |
| `ts/no-unsafe-call` | `off` | relaxed for React component calls |

### General

| Rule | Value | Why |
|------|-------|-----|
| `no-console` | `warn` | flag leftover debug logs |
| `antfu/no-top-level-await` | `off` | allow top-level await (Next.js server components) |
| `node/no-process-env` | `error` | use env abstraction, not raw `process.env` |

### File Naming

| Rule | Value | Why |
|------|-------|-----|
| `unicorn/filename-case` | `error` — `kebabCase` | all files in kebab-case; `README.md` excluded |

### React

| Rule | Value | Why |
|------|-------|-----|
| `style/jsx-max-props-per-line` | `error` — max 1 | one JSX prop per line |
