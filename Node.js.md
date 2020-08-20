# Node.js

## Usage

```bash
node [options] [V8 options] [script.js | -e "script" | -] [--] [arguments]

node inspect [script.js | -e "script" | <host>:<port>] …

node --v8-options

```

## Built-in Modules

- `assert`, `buffer`, `child_process`, `cluster`, `console`, `crypto`, `debugger`, `dgram`, `dns`, `events`, `fs`, `http`, `http2`, `https`, `net`, `os`, `path`, `perf_hooks`, `process`, `querystring`, `readline`, `repl`, `stream`, `string_decoder`, `timers`, `tls`, `tty`, `url`, `util`, `v8`, `vm`, `worker_threads`, `zlib`

## Package Management (npm)

```bash
npm install npm@latest -g # Install latest stable release of npm

# Install package, creates ./node_modules directory
npm [install | i] [<package_name> | <@scope>/<package_name> | <package_name>@<tag>]

npm outdated # List outdated packages

npm update # Update outdated packages

npm uninstall <package_name> # Uninstall package

npm prune [--production] [--dry-run] # Remove extraneous packages
```

CLI flags:

- `-g` install globally
- `-D`, `--save-dev` local development and testing dependencies

### Other Commands

```bash
npm audit # Run a security audit
npm audit fix # Try to fix issues from an audit
npm [bugs | docs | home | issues | repo] # Open browser with package bugs, docs, home, issues or repo
npm ci # Clean, faster non-interactive install
npm config # Set configuration different from package.json config
npm help <term> [<terms..>] # Help
npm [install-ci-test | cit] # npm ci && npm test
npm [install-test | it] # npm install && npm test
npm ls # List installed packages
npm pack [--dry-run] # Create a tarball from a package
npm ping # Ping npm registry
npm [run-script | run] <command> # Run script
npm [search | find | s | se] # Search for packages
npm [[re]start | stop] [-- <args>] # Run restart, start or stop script
npm [test | tst | t] [-- <args>] # Test a package

 # Bump package version, write to package.json, package-lock.json and npm-shrinkwrap.json
 # If package is in git it will also create a version commit and tag
npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease [--preid=<prerelease-id>] \
| from-git] [-m "Commit message with version %s"]
```

### Packages

- Package formats: a directory with `package.json`, `.tar.gz` of the directory, URL to the `.tar.gz`, _name_@_version_, _name_@_tag_, _name_@latest, git URL
- Module: a directory with `package.json` with `main` field, a directory with `index.js`, a JS file
- Readme: root level README.md

#### package.json

```bash
npm init # Create package.json
```

- `name` [a-z_-] and `version` [Semantic Versioning](https://semver.org/) fields are mandatory
- `author` Name <email@example.com> (https://example.com), email and web are optional
- `license` [SPDX License](https://spdx.org/licenses/)
- `description`, `keywords` metadata
- `bugs`, `homepage` links
- `files` contains .gitignore pattern to include files in a package, certain files are always included and excluded, see [npm: npm-package.json](https://docs.npmjs.com/configuring-npm/package-json.html)
- `scripts` contains runable scripts, special meaning has `pre<script>`, `post<script>`, `install`, `test`, `stop`, `restart`, `start`, `version`
- `main`, `browser` primary entry point
- `bin` one or more executable files
- `config` configuration object, usage `process.env.npm_package_config_<key>`
- `dependencies`, `devDependencies`, `peerDependencies`, `bundledDependencies`, `optionalDependencies` - a list of dependencies, version operators `^` / `~` greater than in the same major / minor range, `>`, `<`, `=`, `>=`, `<=`, `-`, `||` and `*`
- `engines`, `os`, `cpu` specifies version of node, os or cpu
- `private: true` won't be published

## See Also

### Cheat Sheets

- [JavaScript Cheat Sheet](JavaScript.md)

## Sources

- [Node.js: Documentation](https://nodejs.org/api/)
- [npm: Documentation](https://docs.npmjs.com/)
- [Semantic Versioning](https://semver.org/)
- [SPDX: License List](https://spdx.org/licenses/)
