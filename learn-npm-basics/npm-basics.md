# `NPM - Basics`

## Fundamentals
1. installation and setup
    - [npm install](https://docs.npmjs.com/cli/v8/commands/npm-install)
    - Verify node and npm version
        ```bash
        node -v
        npm -v
        ```
2. NPM - Configuration
    - [npm config](https://docs.npmjs.com/cli/v8/commands/npm-config)
    ```bash
    npm config list
    ```
    - Common configuration commands
        ```bash
        # Set registry
        npm config set registry https://registry.npmjs.org/

        # Set default author
        npm config set init-author-name "Your Name"
        npm config set init-author-email "your@email.com"

        # View specific config
        npm config get registry
        ```

## Package.json
1. Create a package.json file
    - Initialize a new project
        ```bash
        npm init
        ```
    - Quick initialization (skip questions)
        ```bash
        npm init -y
        ```
2. Package.json structure
    ```json
    {
    "name": "my-project",
    "version": "1.0.0",
    "description": "A sample project",
    "main": "index.js",
    "scripts": {
        "start": "node index.js",
        "test": "jest"
    },
    "keywords": ["sample", "npm"],
    "author": "Your Name",
    "license": "MIT",
    "dependencies": {
        "express": "^4.18.0"
    },
    "devDependencies": {
        "jest": "^29.0.0"
    }
    }
    ```
    - Key Fields explained
        - name: Package identifier (lowercase, no spaces)
        - version: Semantic versioning (major.minor.patch)
        - main: Entry point of your application
        - scripts: Custom commands you can run
        - dependencies: Packages needed in production
        - devDependencies: Packages needed only for development

## Installing packages

1. Installing dependencies
    ```bash
    npm install <package-name>
    # or shortcut
    npm i <package-name>
    ```
    - Dependencies are installed in the node_modules folder
    - If no version is specified, the latest version will be installed
    - If a version is specified, the exact version will be installed
    ```bash
    npm install express@4.18.0
    ```
2. Installing Development Dependencies
    - install as dev dependencies
    ```bash
    npm install --save-dev <package-name>
    # or shortcut
    npm i -D <package-name>
    ```
3. Installing Global packages
    - install as global dependencies
    ```bash 
    npm install -g <package-name>
    # or shortcut
    npm i -g <package-name>
    ```
    - view global packages
    ```bash
    npm list -g

    npm list -g --depth=0
    ```
    - Installation flags
        ```bash
        # Install without saving to package.json
        npm install --no-save <package-name>
        
        # Install exact version (no ^ or ~ )
        npm install --save-exact <package-name>

        # Install from Git repository
        npm install  git+https://github.com/<USER-NAME>/<REPO-NAME>/repo.git

        # Install from local folder
        npm install ../path/to/local/folder
        ``` 

## Semantic Versioning
1. Understanding Semantic Versioning
    Format `MAJOR.MINOR.PATCH`
    - MAJOR: Breaking changes (incompatible API changes)
    - MINOR: New features (backwards compatible)
    - PATCH: Bug fixes (backwards compatible)
2. Version Symbols
    ```json
    {
    "dependencies": {
        "express": "4.18.2",      // Exact version
        "mongoose": "^6.0.0",     // Compatible with 6.x.x (most common)
        "lodash": "~4.17.0",      // Compatible with 4.17.x
        "axios": "*",             // Any version (not recommended)
        "moment": ">=2.0.0",      // Greater than or equal
        "chalk": "2.x",           // Any 2.x.x version
        "dotenv": "latest"        // Latest version (risky)
        }
    }
    ```
3. Caret (^) vs Tilde (~)
    - **caret(^):** Updates minor and patch versions
        - `^1.2.3` Allows 1.2.4, 1.3.0, but not 2.0.0
    - **tilde(~):** Updates only patch versions
        - `~1.2.3` Allows 1.2.3, 1.2.4, but not 1.3.0

## Package-lock.json
1. Package-lock.json is a file that contains the exact versions of all the dependencies in your project.
- It ensures:
    - **Deterministic Installs:** Same dependency trees across all environments
    - **Faster Installs:** Cached dependecy resolution
    - **Security:** Locks down specific versions of dependencies including sub-dependencies

```json
{
    "name": "my-project",
    "version": "1.0.0",
    "lockfileVersion": 3,
    "dependencies": {
        "express": {
        "version": "4.18.2",
        "resolved": "https://registry.npmjs.org/express/-/express-4.18.2.tgz",
        "integrity": "sha512-...",
        "requires": {
            "body-parser": "1.20.1",
            "cookie": "0.5.0"
            }
        }
    }
}
```

2. Best practices
    - **Always commit** package-lock.json to version control
    - Never edit manually
    - If corrupted, delete and run ```npm install```

## NPM Scripts
1. What are scripts?
    - Scripts are command-line shorcuts that you define in your `package.json` file. They automate tasks and improve your workflow.
    - Scripts can be run using the `npm <script-name>` command, or the `npm run <script-name>` command.

2. Basic Scripts
    ```json
    {
        "scripts": {
            "start": "node server.js",
            "dev": "nodemon server.js",
            "test": "jest",
            "build": "webpack"
        }
    }
    ```
    - `npm run start` will run the `start` script
3. List of common scripts
    - `start`: Run the application, production server
    - `dev`: Run server with auto restart on changes (needs nodemon)
    - `test`: Run all tests once
    - `test:watch`: Run all tests and watch for changes
    - `test:coverage`: Run all tests and generate coverage report
    - `lint`: Check code for style/error issues
    - `lint:fix`: Fix style/error issues
    - `format`: Format code with Prettier
    - `build`: Bundle the application for production
    - `clean`: Delete generated files
    - `docs`: Generate documentation
    - `deploy`: Deploy the application to production
4. chaining scripts
    - Sequentian execution one after another, stops if one fails
    ```json
    {
        "scripts": {
            "clean": "rm -rf dist",
            "build": "webpack",
            "test": "jest",
            "deploy": "npm run clean && npm run build && npm run test" 
        }
    }
    ```
5. Best practices for NPM scripts
    - **Use descriptive names**: `build:prod` instead of `bd`
    - **Document complex scripts**: add comments in README.md
    - **Keep it simple**: Don't overcomplicate scripts
    - **Avoid side effects**: Don't use scripts that modify files outside of the project
    - **Use Conventions**: 
        - `test` for tests
        - `lint` for linting
        - `build` for building
        - `deploy` for deploying
    - **Always commit package.json**. Scripts are part of your project's documentation

## Managing Packages
1. Updating Packages
    - check for updates: `npm outdated`
    - update a specific package: `npm update <package-name>`
    - update all packages: `npm update`
    - updating to latest (ignoring semver): `npm update <package-name>@latest`

2. Uninstalling Packages
    - uninstall a specific package: `npm uninstall <package-name>`
    - uninstall all packages: `npm uninstall`
    - Remove dev dependency: `npm uninstall -D <package-name>`
    - Remove global dependency: `npm uninstall -g <package-name>`

3. Viewing packages Info
    - view package details: `npm view <package-name>`
    - view package details with versions: `npm view <package-name> versions`
    - view package in browser:
        - `npm repo <package-name>`
        - `npm docs <package-name>`

4. Listing Packages
    - view all installed packages: `npm list`
    - view all installed packages with versions: `npm list --depth=0`
    - view all installed packages with dependencies: `npm list --depth=0 --prod`
    - List specific package: `npm list <package-name>`

## NPM Cache 