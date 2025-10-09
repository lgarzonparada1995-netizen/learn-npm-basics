# 📦 Learn NPM Basics

Welcome to **Learn NPM Basics** — a beginner-friendly guide to understanding and mastering **npm (Node Package Manager)**.  
This repository will teach you what npm is, how to use it effectively, and introduce the **most important commands** with practical examples and exercises.

---

## 🚀 What You’ll Learn

By working through this repo, you’ll understand:

- What **npm** is and why it’s used
- How to **install and manage packages**
- The structure and purpose of the **package.json** file
- How to use the most common **npm commands**
- How to **create and publish your own npm package**
- Common **troubleshooting tips** and **best practices**

---

## 📚 Topics Covered

1. **Introduction to npm**
   - What is npm?
   - Installing Node.js and npm
   - Checking your npm version

2. **Working with Packages**
   - Installing local and global packages
   - Removing and updating packages
   - Using `npx`

3. **Understanding `package.json`**
   - Scripts section
   - Dependencies vs devDependencies
   - Semantic versioning (`^`, `~`, exact versions)

4. **Useful Commands**
   - `npm init` – Create a new project
   - `npm install` – Install all dependencies
   - `npm uninstall` – Remove packages
   - `npm update` – Update packages
   - `npm list` – View installed packages
   - `npm run` – Run custom scripts

5. **Publishing Packages**
   - Creating an npm account
   - Setting up a publishable package
   - Publishing and unpublishing

6. **Practice Exercises**
   - Installing and removing dependencies
   - Editing scripts in `package.json`
   - Creating and publishing a test package

---

## 🧠 Example

```bash
# Initialize a new Node.js project
npm init -y

# Install a package
npm install lodash

# Use the package in your code
node -e "const _ = require('lodash'); console.log(_.capitalize('hello npm!'));"
```

---

## 🧩 Exercises

Try the following tasks to reinforce your learning:

1. Create a project and install **Express**.
2. Add a script called `"start"` that runs `node app.js`.
3. Create a `package.json` file manually and understand each section.
4. Publish a dummy package to npm (optional).

---

## 💡 Tips

- Always run `npm install` after cloning a new project.
- Use `npm outdated` to check for newer versions.
- Use `.npmrc` for custom configurations.

---

## 🛠 Requirements

- Node.js (v18 or higher recommended)
- npm (comes with Node.js)

Check installation:

```bash
node -v
npm -v
```

---

## 🤝 Contributing

Feel free to open issues, suggest improvements, or submit pull requests!  
Contributions and examples are always welcome.

---

## 🧾 License

This project is licensed under the **MIT License**.  
See the [LICENSE](LICENSE) file for details.

---

Happy learning! 🎯
