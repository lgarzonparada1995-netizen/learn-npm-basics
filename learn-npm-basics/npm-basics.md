# NPM - Notes

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

# Installing packages

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