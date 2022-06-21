# Tauri Svelte Template

- Tauri
- GitHub action for cross-platform builds
- Svelte
- Vite
- TypeScript
- `svelte-preprocess` with Sass installed by default
- Hot module replacement
- ESLint
- Prettier

## Dev instructions

### Get started

1. Install Node.js
2. Install Rust
3. Follow the [Tauri setup guide](https://tauri.studio/en/docs/get-started/intro)
4. Run `npm install`

### Commands
- `npm run dev`: Start app in dev mode
- `npm run build`: Build
- `npm run lint`: Lint
- `npm run format`: Format

### Release new version
1. Update `CHANGELOG.md`
2. Bump the version number in `src-tauri/Cargo.toml`
3. Run `npm run check` to update `Cargo.lock`
4. Create a git tag in the format `v#.#.#`
5. Add release notes to the generated GitHub release and publish it

```
git clone git@github.com:probablykasper/tauri-svelte-template.git
cd tauri-svelte-template
pnpm i
// update tauri-apps and tauri-cli to the latest
pnpm i -D @tauri-apps/cli@latest
pnpm i -D @tauri-apps/api@latest
// 
rm src-tauri/Cargo.lock
// update Cargo.lock
cargo update
// check if it works
pnpm run build
pnpm run dev
pnpm run dev:web
// installing tailwind, flowbite, flowbite-svelte
pnpm i -D flowbite-svelte@latest
npx svelte-add@latest tailwindcss
pnpm i
pnpm i -D flowbite
// see in a browser
pnpm run dev:web
```
