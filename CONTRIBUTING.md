# Welcome Contributors! 🎉

Welcome to the Electricity Maps open source contribution repository. </br>

Electricity Maps helps people around the world understand the emission of the electricity in their country. At Electricity Maps we believe information precedes action, as such, to push changes regarding electricity emissions, people need to understand them.

Any and all contributions however big or small are welcome.

## Links

- [README][readme]
- [Code of Conduct][code of conduct]
- [License][license]
- [Wiki][wiki]
- Our [Website](https://www.electricitymaps.com)
- Our [API Docs](https://static.electricitymaps.com/api/docs/index.html)
- Join us on Slack at http://slack.electricitymaps.com to see what we are working on and to get in touch with other contributors.
- Our [data sources](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/DATA_SOURCES.md)
- How to [verify data sources](https://github.com/electricitymaps/electricitymaps-contrib/wiki/Verify-data-sources) 

## Code of Conduct

This repository and by extension its community have adopted the [Contributor Covenant][contributor covenant] v2.1 as its code of conduct.
If you have any questions about the code of conduct or feel the need to report an incident you can do so by emailing us at codeofconduct@electricitymaps.com. For the full code of conduct see [CODE_OF_CONDUCT.md][code of conduct].

## License

We use the GNU Affero General Public License v3.0 for this repository, check the [LICENSE.md][license] file details about what exactly this entails. Contributions prior to commit [cb9664f][commit cb9664f] were licensed under [MIT license][old_license]

## Getting Started

How do I contribute?

1) Navigate to our repository's code and click [Fork](https://help.github.com/articles/fork-a-repo/) near the top right
2)  [Clone](https://help.github.com/articles/cloning-a-repository/) your fork of the repository by clicking the green "Code" dropdown in your fork of the project then choose your preferred cloning method from the options. (Note: this should be done in <yourGithubUsername>/electricitymaps-contrib) repository. 
3) Set up your local environment (follow instructions in section below)
4) Make your code changes and test them in your local environment.
5. [Push](https://github.com/git-guides/git-push) your changes to your fork.
6. Submit a [pull request](https://help.github.com/articles/using-pull-requests/) to bring your contribution into the production version.


## Set up your local environment:

### Setup Python development environment

1. Ensure you are using Python 3.10 (We recommend using [pyenv](https://github.com/pyenv/pyenv) to handle different Python versions.)

2. Ensure you have the dependency management tool [Poetry](https://python-poetry.org) installed by this [guide](https://python-poetry.org/docs/#installation). The easiest is to do `pip install poetry`

3. Ensure you have the dependency tool tesseract installed, following the instructions in [this guide](https://github.com/tesseract-ocr/tesseract).

4. From the root folder, install the dependencies in a virtual environment:
   ```
   poetry install -E parsers
   ```

You can now run a few different commands:
```
poetry run lint # linting
poetry run test # run unit tests
poetry run check # run both linting and tests
```

You might need to have `zlib` and `libjpeg` installed on your machine.

To ensure all dependencies required by opencv are installed, you can run `apt-get update && apt-get install -y python3-opencv`

### Having problems?

First up, make sure you're using Python `3.10`. Also, see [Troubleshooting](https://github.com/tmrowco/electricitymap-contrib/wiki/Troubleshooting) for fixes to common issues.

If it's still not working, please create an issue where you include the output from `poetry debug` so that we can help debug it.

### Setup frontend environment
1. Ensure you have [nodejs](https://nodejs.org/) 18 or higher installed.
2. Run: 

   ```bash
   sudo npm install --global pnpm
   ```
3. In the web folder run:

   ```bash
   pnpm install
   ```
3. Do the same from the mockserver folder:

   ```bash
   pnpm install
   ```

### Running the frontend map
There are two ways to run the frontend map the quickest and easiest way is to use the vite dev server and the second way is to use build to create a full production build, the later is only recommended when testing the build pipeline.
#### Vite development server
1. Run the following command in the web folder:

   ```bash
   pnpm run dev
   ```
2. Go to [http://localhost:5173/](http://localhost:5173/) and you should see the map!
3. Color the map by opening a new terminal in the web folder and starting the mockserver with the following command:

   ```bash
   pnpm run mockserver
   ```

### Vite production build
1. Provide a value for the required environment variables, listed [here](https://github.com/electricitymaps/electricitymaps-contrib/blob/master/web/README.md#building-for-production). These can be set in a [.env](https://vitejs.dev/guide/env-and-mode.html#env-files) file inside the web folder.

2. Run the following command in the web folder:

   ```bash
   pnpm run build
   ```

3. Start the preview server with:
   
   ```bash
   pnpm run preview
   ```
Notes:
   - The backend handles the calculation of carbon emissions. The map data from the mock server provides dummy data from the [state file](https://github.com/tmrowco/electricitymap-contrib/blob/master/mockserver/public/v6/state).

See [Troubleshooting](https://github.com/tmrowco/electricitymap-contrib/wiki/Troubleshooting) for common issues and fixes when building the map locally.

## Code formatting

Your code contributions can't be merged with the codebase unless they respect the electricityMap contrib code formatting.

To check whether you code respects the formatting, you can run the following commands:
### Python
```bash
poetry run check
```

If you see that your code fails the formatting check, you can autoformat it by running:

```bash
poetry run format
```
### JavaScript, JSON, CSS, YML and more:
```bash
npx prettier --check .
```
And if the check fails you can run the following command to fix it:
```bash
npx prettier --write .
```

## Non-code contributions

There are several ways to help out without coding, these are primarily:

- Opening issues for bugs.
- Opening issues for data problems.
- Opening and/or participating in discussions about new data sources, features, and more.
- Opening issues when capacity data sources have been updated or changed.
- Finding new data sources, wiki page: [Find data sources][wiki find data sources]
- Verify existing data sources, wiki page: [Verify data sources][wiki verify data sources]
- Adding new or updating our existing translations, wiki page: [Translating app.electricitymaps.com][wiki translating the app]
- And more!


## Zone and exchange configurations

Static information about zones and exchanges are located at [config/zones][config zones] and [config/exchanges][config exchanges] respectively.
The zone configurations hold information such as the installed capacity, which parsers to use, fallback mixes, contributors and other keys that are required by our frontend and internal systems; and while similar the exchange configs hold the the location, capacity, direction and parsers required.

## Parser guidelines

To get started with editing the parsers use the following steps:

1. Run `poetry install -E parsers` to install all needed dependencies.
2. Use `poetry run test_parser ZONE_KEY` to test any parser changes.

Note: This requires you to have [Python 3.10][python homepage] and [Poetry][poetry homepage] installed, you can see their respective installation guides here:

- [Downloading Python][python install guide]
- [poetry installation][poetry install guide]

### Parser information

For more detailed information about parsers specifically you can look at the parser [README][parser readme] located at [parsers/README.md][parser readme] with specific information about the parser functions located in the [parser/example][parser examples folder] folder

#### Example parser:

For an example of how a parser can look we have an example here: </br> [parsers/examples/example_parser.py][example parser]

### Formatting the parsers

We use [black][black homepage] and [isort][isort homepage] as code formatters for python which is automatically checked in the CI job `Python / Formatting`.

If this jobs fails and you need to manually format the code you can run `poetry run format` in the top level of the repository.

Check the [wiki page][wiki python code formatting] for more details and tips.

## Front-end guidelines

To get started with editing the frontend use the following steps:

1. Use `cd web` to go into the web directory
2. Then use `pnpm install` to get all dependencies installed.

Note: This requires you to have [node.js][node homepage] and [pnpm][pnpm homepage] installed, you can see their respective installation guides here:

- [How to install node.js][node installation guide]
- [pnpm installation][pnpm installation guide]

### Frontend structure

The frontend can be broken down into 2 main parts, the web app built [Vite][vitejs] and the mobile app built with [capacitor][capacitorjs].
Both of these share a common code base that is built upon [react][reactjs].

As a result we have a frontend folder structure that looks like this:

```
mobileapp
├── android
├── assets
├── icons
└──ios
web
├── config
├── cypress
├── geo
├── public
├── scripts
└── src
    ├── api
    ├── components
    ├── features
    ├── hooks
    ├── stories
    ├── testing
    ├── translation
    └── utils
```

### State management

We use [Jotai][jotai homepage] that saves our state in primitive atoms, these live in #TODO: LINK TO ATOM FILE WHEN REWRITE IS MERGED and are then imported in the individual frontend files where it's needed. If you have a need to save the state for a new feature you should add a new atom to this file so we keep everything organized.

### Formatting the frontend

The frontend uses [ESLint][eslint homepage] and [Prettier][prettier homepage] as formatters for all code and this is automatically checked in the CI jobs `Prettier / Check` and `ESLint / Check`.

If these jobs fail and you need to format the code you can run `yarn lint --fix` in the `/web` folder to do so.

Check the [wiki page][wiki js code formatting] on formatting for more details and tips.

# Need Help? Follow these steps:
1) Check out our [Wiki](https://github.com/electricitymaps/electricitymaps-contrib/wiki) and [Discussions]x(https://github.com/electricitymaps/electricitymaps-contrib/discussions)
2) Review Environment Setup again (seen above and in our Wiki)
3) Check our [Troubleshooting Guide](https://github.com/electricitymaps/electricitymaps-contrib/wiki/Troubleshooting)
4) Ask us a question on [Slack](http://slack.electricitymaps.com) or start a new [Discussion](https://github.com/electricitymaps/electricitymaps-contrib/discussions)
5) Create a draft Pull Request - The easiest way for getting other people to look at your code would be to open a draft pull request. We'd rather have one draft too many. Make sure to state exactly what your issue is, so it's easy for other contributors to help out. Opening a PR will automatically send a message in Slack.


<!-- Link definitions to keep the text clean -->

[poetry homepage]: https://python-poetry.org/
[python homepage]: https://www.python.org/
[python install guide]: https://wiki.python.org/moin/BeginnersGuide/Download
[poetry install guide]: https://python-poetry.org/docs/#installation
[example parser]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/parsers/examples/example_parser.py
[black homepage]: https://github.com/psf/black
[isort homepage]: https://pycqa.github.io/isort/
[wiki python code formatting]: https://github.com/electricitymaps/electricitymaps-contrib/wiki/Format-your-code-contribution#python-code-formatting
[node homepage]: https://nodejs.org/
[pnpm homepage]: https://pnpm.io/
[node installation guide]: https://nodejs.dev/en/learn/how-to-install-nodejs/
[pnpm installation guide]: https://pnpm.io/installation
[jotai homepage]: https://jotai.org/
[eslint homepage]: https://eslint.org/
[prettier homepage]: https://prettier.io/
[wiki js code formatting]: https://github.com/electricitymaps/electricitymaps-contrib/wiki/Format-your-code-contribution#js-code-formatting
[wiki translating the app]: https://github.com/electricitymaps/electricitymaps-contrib/wiki/Translating-app.electricitymaps.com
[reactjs]: https://reactjs.org/
[vitejs]: https://vitejs.dev/
[capacitorjs]: https://capacitorjs.com/
[readme]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/README.md
[code of conduct]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/CODE_OF_CONDUCT.md
[license]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/LICENSE.md
[wiki]: https://github.com/electricitymaps/electricitymaps-contrib/wiki
[wiki find data sources]: https://github.com/electricitymaps/electricitymaps-contrib/wiki/Find-data-sources
[wiki verify data sources]: https://github.com/electricitymaps/electricitymaps-contrib/wiki/Verify-data-sources
[contributor covenant]: https://www.contributor-covenant.org/
[commit cb9664f]: https://github.com/electricitymaps/electricitymaps-contrib/commit/cb9664f43f0597bedf13e832047c3fc10e67ba4e
[old_license]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/LICENSE_MIT.txt
[config zones]: https://github.com/electricitymaps/electricitymaps-contrib/tree/master/config/zones
[config exchanges]: https://github.com/electricitymaps/electricitymaps-contrib/tree/master/config/exchanges
[parser readme]: https://github.com/electricitymaps/electricitymaps-contrib/tree/master/parsers/README.md
[parser examples folder]: https://github.com/electricitymaps/electricitymaps-contrib/blob/master/parsers/examples/
