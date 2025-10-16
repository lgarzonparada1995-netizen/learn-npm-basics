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
1. Understanding NPM Cache
    - NPM Cache stores downloaded packages in a local directory
    - NPM Cache is used to speed up package installation and reduce network traffic
    - View NPM Cache location: `npm config get cache`

2. Cache Commands
    ```bash
    # Verify cache integrity
    npm cache verify

    # Clear cache
    npm cache clean --force

    # View cache content
    npm cache list
    ```

## Security & Audit
1. Understanding Security and Audit
    - NPM has a built-in security audit feature that checks for vulnerabilities in installed packages
    - Run audit: `npm audit`
    - View audit report: `npm audit --json`

2. Fixing Security Vulnerabilities
    - Fix vulnerabilities: `npm audit fix`
    - Fix with breaking chancges: `npm audit fix --force`

3. Security best practices
    ```bash
    # Chek specific packages
    npm vie <package-name> security

    # Install only production dependencies
    npm install --omit=dev

    # Verify package integrity
    npm install --integrity
    ```

## Publishing Packages
1. Understanding Publishing
    - NPM has a built-in publish feature that allows you to publish your packages to the registry
    - why publish pakages?
        - Share reusable code with other developers
        - Use your own utilities across multiple projects
        - Contribute to open source projects
        - Build your portfolio
        - Establish expertise in a domain

2. Type of packages
    1. **Public packages**: Anyone can insttall (free)
    2. **Scoped packages**: Only users with access can install, namespace under your username (paid)
    3. **Private packages**: Only you or your team  can install (requires paid NPM account)
    4. **Organization packages**: Share within an organization (requires paid NPM account)

3. Prereqisites before starting creating packages
    1. <u>**Create an NPM account**</u>:
        - https://www.npmjs.com/signup
        - Choose a username and password
        - Verify your email address 
    2. <u>**Login via CLI**</u>:
        ```bash
        npm login
        ```
        You'll be prompted for :
        - Username
        - Password
        - Email
        - Two-factor authentication (if enabled)

        Verify you're logged in:
        ```bash
        npm whoami
        ```

4. Preparing your package step by step
Let's create a real package from scratch. We'll build a simple string utility library.
    1. <u>Create project structured</u>
        ```bash
        mkdir awesome-string-utils
        cd awesome-string-utils
        npm init
        ```
    2. <u>Answer the prompts carefully</u>
        ```markdown
        package name: (awesome-string-utils)
        @your-username/awesome-string-utils
        version: (1.0.0)
        description: Handy string manipulation utilities
        entry point: (index.js)
        test command: jest
        git repository: (https://github.com/your-username/awesome-string-utils.git)
        keywords: (string, utilities, manipulation, helpers, text)
        author: (Your Name) <your@email.com>
        license: (ISC) MIT
        ```
        why these choices matter:
        - Name with scope `@your-username/` Always available, avoids naming conflicts
        - description: First thing people see when searching NPM
        - entry point: Main file of the package, that exports your functionality
        - keywords: Help people find your package
        - license: MIT License is most permissive and popular

5. Complete package.json explained
    - Here's and example of a complete professional package.json file:
        ```json
        {
            "name": "@your-username/awesome-string-utils",
            "version": "1.0.0",
            "description": "Handy string manipulation utilities",
            "main": "index.js",
            "scripts": {
                "test": "jest",
                "test:watch": "jest --watch",
                "test:coverage": "jest --coverage",
                "lint": "eslint .",
                "lint:fix": "eslint . --fix",
                "format": "prettier --write ."
                "prepublishOnly": "npm run lint && npm run format"
            },
            "repository": {
                "type": "git",
                "url": "https://github.com/your-username/awesome-string-utils.git"
            },
            "keywords": [
                "string",
                "utilities",
                "manipulation",
                "helpers",
                "text"
            ],
            "author": "Your Name <your@email.com>",
            "license": "MIT",
            "repository": {
                "type": "git",
                "url": "https://github.com/your-username/awesome-string-utils.git"
            },
            "bugs": {
                "url": "https://github.com/your-username/awesome-string-utils/issues"
            },
            "homepage": "https://github.com/your-username/awesome-string-utils#readme",
            "engines": {
                "node": ">=12",
                "npm": ">=6"
            },
            "files": [
                "index.js",
                "lib/",
                "README.md",
                "LICENSE"
            ],
            "dependencies": {},
            "devDependencies": {
                "eslint": "^8.0.0",
                "eslint-config-prettier": "^8.0.0",
                "eslint-plugin-jest": "^27.0.0",
                "eslint-plugin-prettier": "^4.0.0",
                "jest": "^27.0.0",
                "prettier": "^2.0.0"
            }       
        }
        ```
    - Line by line explanation:
        - `name`: Package identifier (lowercase, no spaces)
        - `version`: Semantic versioning (major.minor.patch)
        - `description`: Shows up in search results - make it clear and consice
        - `main`: Main file of the package, that exports your functionality. what gets loaded when someone requires your package
        - `scripts`: Commands for running tests, linting, formatting, etc.
        - `repository`: Link to your package on GitHub