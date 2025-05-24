# Monorepo: React + Angular + Storybook + GitHub Pages Deployment

This monorepo hosts two applications:

- `apps/react-app`: A React application
- `apps/angular-app`: An Angular application

It uses **NPM Workspaces** for dependency management and **GitHub Actions** to deploy each app to separate GitHub Pages repositories.

---

## 🧱 Folder Structure

```

my-monorepo/
├── packages/
│   ├── react-storybook/        # React App with Storybook
│   └── angular-storybook/      # Angular App with Storybook
├── .github/
│   └── workflows/
│       └── deploy.yml    # Deploy workflow for both apps
├── package.json          # Root config with workspaces
└── node\_modules/

````

---

## 🚀 Setup

### 1. Install dependencies (from root)

```bash
npm install
```

> Uses NPM workspaces to install all dependencies at the root.

---

## 📦 Scripts

### React App

```bash
npm run sb-react
npm run sb-build-react
```

### Angular App

```bash
npm run sb-angular
npm run sb-build-angular
```

---

## 🚀 Deployment (via GitHub Actions)

This monorepo pushes builds to two separate repositories:

| App     | Repo                 | Deployed To                                             |
| ------- | -------------------- | ------------------------------------------------------- |
| React   | [`react-app-deploy`](https://github.com/pratik-pdw/react-app-deploy)   | [https://pratik-pdw.github.io/react-app-deploy](https://pratik-pdw.github.io/react-app-deploy)   |
| Angular | [`angular-app-deploy`](https://github.com/pratik-pdw/angular-app-deploy) | [https://pratik-pdw.github.io/angular-app-deploy](https://pratik-pdw.github.io/angular-app-deploy) |

### Trigger

On every push to `main` branch of this monorepo, GitHub Actions will:

* Build each app
* Push the build output to the `gh-pages` branch of the respective deploy repo
* Overwrite old content in the deploy branch

### Personal Access Token

Add a secret named `DEPLOY_TOKEN` in this repository (`mono-repo`) with a fine-grained personal access token that has:

* Access to `react-app-deploy` and `angular-app-deploy`
* `contents: read and write` permission

---

## 🧪 Storybook Access (local dev)

After running Storybook:

* Angular: [http://localhost:6006](http://localhost:6006)
* React: [http://localhost:6007](http://localhost:6007)

---

## 🔧 Notes

* Uses `peaceiris/actions-gh-pages` for clean deployment
* React app must set `"homepage"` in its `package.json`
* Angular app must be built with `--base-href=/angular-app-deploy/`
* No need to run `npm install` inside each app — root install handles everything via workspaces

