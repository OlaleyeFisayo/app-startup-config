# ESLint Config Reference

Built on [`@antfu/eslint-config`](https://github.com/antfu/eslint-config).

## General Config

```ts
// eslint.config.mjs
import antfu from "@antfu/eslint-config";
import tanstackPluginQuery from "@tanstack/eslint-plugin-query";

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
    // tanstack query integration
    plugins: { "@tanstack/query": tanstackPluginQuery },

    rules: {
      // tanstack query integration
      ...tanstackPluginQuery.configs.recommended.rules,

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
      "node/prefer-global/process": "off",
      "ts/no-misused-promises": "off",

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
