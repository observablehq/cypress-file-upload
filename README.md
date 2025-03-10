# cypress-file-upload

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/abramenal/cypress-file-upload/blob/master/LICENSE) [![npm version](https://img.shields.io/npm/v/cypress-file-upload.svg?style=flat&color=important)](https://www.npmjs.com/package/cypress-file-upload) [![CircleCI Status](https://circleci.com/gh/abramenal/cypress-file-upload.svg?style=shield)](https://circleci.com/gh/abramenal/cypress-file-upload) [![All Contributors](https://img.shields.io/badge/all_contributors-30-yellow.svg)](#contributors)

File upload testing made easy.

This package adds a custom [Cypress][cypress] command that allows you to make an abstraction on how exactly you upload files through HTML controls and focus on testing user workflows.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [API](#api)
- [Recipes](#recipes)
- [Caveats](#caveats)
- [It isn't working! What else can I try?](#it-isnt-working-what-else-can-i-try)
- [Contributors](#contributors)
- [License](#license)

## Installation

The package is distributed via [npm][npm] and should be installed as one of your project's `devDependencies`:

```bash
npm install --save-dev cypress-file-upload
```

## Usage

`cypress-file-upload` extends Cypress' `cy` command.
Add this line to your project's `cypress/support/commands.js`:

```javascript
import 'cypress-file-upload';
```

Now you are ready to actually test uploading. Here is an example with HTML5 file input:

```javascript
const fileName = 'data.json';

cy.fixture(fileName).then(fileContent => {
  cy.get('[data-cy="file-input"]').upload({ fileContent, fileName, mimeType: 'application/json' });
});
```

And a similar one for custom drag-n-drop component:

```javascript
const fileName = 'data.json';

cy.fixture(fileName).then(fileContent => {
  cy.get('[data-cy="dropzone"]').upload(
    { fileContent, fileName, mimeType: 'application/json' },
    { subjectType: 'drag-n-drop' },
  );
});
```

**Trying to upload a file that does not supported by Cypress by default?** Make sure you pass `encoding` property (see [API](#api)).

See more usage guidelines in [recipes](./recipes).

## API

Exposed command in a nutshell:

```javascript
cySubject.upload(fileOrArray, processingOpts);
```

`fileOrArray` is an object (or an array of those) that represents file information and contains following properties:

- {String} `fileContent` – raw file content, usually a value obtained from [`cy.fixture`][cy.fixture]
- {String} `fileName` – file name (with extension)
- {String} `mimeType` – file [MIME][mime] type
- {String} `encoding` – (optional) normally [`cy.fixture`][cy.fixture] resolves encoding automatically, but in case it cannot be determined you can provide it manually. For a list of allowed encodings, see [here](https://github.com/abramenal/cypress-file-upload/blob/master/src/constants.js#L29)

`processingOpts` (optional) contains following properties:

- {String} `subjectType` – target (aka subject) element kind: `'drag-n-drop'` component or plain HTML `'input'` element. Defaults to `'input'`
- {String} `subjectNature` – target element nature: `'dom'` represents regular DOM elements, `'shadow'` stands for using elements within Shadow DOM. Defaults to `'dom'`
- {Boolean} `force` – (optional) same as for [`cy.trigger`][cy.trigger] it enforces events triggering on HTML subject element. Usually this is necessary when you use hidden HTML controls for your file upload. Defaults to `false`

## Recipes

Most common frontend UI setups along with Cypress & file upload testing are located at [recipes](./recipes).

Any contributions are welcome!

## Caveats

During the lifetime plugin faced some issues you might need to be aware of:

- Chrome 73 changes related to HTML file input behavior: [#34][#34]
- Force event triggering (same as for [`cy.trigger`][cy.trigger]) should happen when you use hidden HTML controls: [#41][#41]
- Binary fixture has a workarounded encoding: [#70][#70]
- Shadow DOM compatibility: [#74][#74]
- Reading file content after upload: [#104][#104]

## It isn't working! What else can I try?

Here is step-by-step guide:

1. Check [Caveats](#caveats) – maybe there is a tricky thing about exactly your setup
1. Submit the issue and let us know about you problem
1. In case you're using a file with encoding and/or extension that is not yet supported by Cypress, make sure you've tried to explicitly set the `encoding` property (see [API](#api))
1. Comment your issue describing what happened after you've set the `encoding`

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/all-contributors/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/allout58"><img src="https://avatars0.githubusercontent.com/u/2939703?v=4" width="100px;" alt="James Hollowell"/><br /><sub><b>James Hollowell</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=allout58" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/lunxiao"><img src="https://avatars1.githubusercontent.com/u/17435809?v=4" width="100px;" alt="lunxiao"/><br /><sub><b>lunxiao</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Alunxiao" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://www.ollie-odonnell.com"><img src="https://avatars2.githubusercontent.com/u/5886107?v=4" width="100px;" alt="Oliver O'Donnell"/><br /><sub><b>Oliver O'Donnell</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Aoliverodaa" title="Bug reports">🐛</a> <a href="https://github.com/abramenal/cypress-file-upload/commits?author=oliverodaa" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/virtuoushub"><img src="https://avatars0.githubusercontent.com/u/4303638?v=4" width="100px;" alt="Peter Colapietro"/><br /><sub><b>Peter Colapietro</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=virtuoushub" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/km333"><img src="https://avatars1.githubusercontent.com/u/37389351?v=4" width="100px;" alt="km333"/><br /><sub><b>km333</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Akm333" title="Bug reports">🐛</a></td>
    <td align="center"><a href="http://pages.cs.wisc.edu/~mui/"><img src="https://avatars2.githubusercontent.com/u/17896701?v=4" width="100px;" alt="Kevin Mui"/><br /><sub><b>Kevin Mui</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=kmui2" title="Code">💻</a> <a href="#ideas-kmui2" title="Ideas, Planning, & Feedback">🤔</a> <a href="#review-kmui2" title="Reviewed Pull Requests">👀</a></td>
    <td align="center"><a href="http://www.benwurth.com/"><img src="https://avatars0.githubusercontent.com/u/2358786?v=4" width="100px;" alt="Ben Wurth"/><br /><sub><b>Ben Wurth</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Abenwurth" title="Bug reports">🐛</a> <a href="https://github.com/abramenal/cypress-file-upload/commits?author=benwurth" title="Code">💻</a></td>
  </tr>
  <tr>
    <td align="center"><a href="http://tomskjs.ru"><img src="https://avatars2.githubusercontent.com/u/1303845?v=4" width="100px;" alt="Andreev Sergey"/><br /><sub><b>Andreev Sergey</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=DragorWW" title="Tests">⚠️</a> <a href="#question-DragorWW" title="Answering Questions">💬</a> <a href="#example-DragorWW" title="Examples">💡</a> <a href="https://github.com/abramenal/cypress-file-upload/commits?author=DragorWW" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/GuillaumeDind"><img src="https://avatars1.githubusercontent.com/u/45589123?v=4" width="100px;" alt="Guts"/><br /><sub><b>Guts</b></sub></a><br /><a href="#question-GuillaumeDind" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://github.com/maple-leaf"><img src="https://avatars3.githubusercontent.com/u/3980995?v=4" width="100px;" alt="maple-leaf"/><br /><sub><b>maple-leaf</b></sub></a><br /><a href="#question-maple-leaf" title="Answering Questions">💬</a> <a href="https://github.com/abramenal/cypress-file-upload/commits?author=maple-leaf" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/daniula"><img src="https://avatars3.githubusercontent.com/u/91628?v=4" width="100px;" alt="Daniel Mendalka"/><br /><sub><b>Daniel Mendalka</b></sub></a><br /><a href="#question-daniula" title="Answering Questions">💬</a></td>
    <td align="center"><a href="http://www.stickypixel.com"><img src="https://avatars1.githubusercontent.com/u/12176122?v=4" width="100px;" alt="Chris Sargent"/><br /><sub><b>Chris Sargent</b></sub></a><br /><a href="#question-ChrisSargent" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://ronakchovatiya.glitch.me/"><img src="https://avatars1.githubusercontent.com/u/16197756?v=4" width="100px;" alt="Ronak Chovatiya"/><br /><sub><b>Ronak Chovatiya</b></sub></a><br /><a href="#question-rchovatiya88" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://geromekevin.com"><img src="https://avatars0.githubusercontent.com/u/31096420?v=4" width="100px;" alt="Jan Hesters"/><br /><sub><b>Jan Hesters</b></sub></a><br /><a href="#question-janhesters" title="Answering Questions">💬</a> <a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Ajanhesters" title="Bug reports">🐛</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/skjnldsv"><img src="https://avatars0.githubusercontent.com/u/14975046?v=4" width="100px;" alt="John Molakvoæ"/><br /><sub><b>John Molakvoæ</b></sub></a><br /><a href="#question-skjnldsv" title="Answering Questions">💬</a></td>
    <td align="center"><a href="http://psjones.co.uk"><img src="https://avatars1.githubusercontent.com/u/677167?v=4" width="100px;" alt="Phil Jones"/><br /><sub><b>Phil Jones</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Aphiljones88" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/NicolasGehring"><img src="https://avatars3.githubusercontent.com/u/38431471?v=4" width="100px;" alt="Nicolas Gehring"/><br /><sub><b>Nicolas Gehring</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3ANicolasGehring" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://www.pertiller.tech"><img src="https://avatars3.githubusercontent.com/u/1514111?v=4" width="100px;" alt="David Pertiller"/><br /><sub><b>David Pertiller</b></sub></a><br /><a href="#question-Mobiletainment" title="Answering Questions">💬</a> <a href="https://github.com/abramenal/cypress-file-upload/commits?author=Mobiletainment" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/xiaomeidan"><img src="https://avatars1.githubusercontent.com/u/5284575?v=4" width="100px;" alt="Amy"/><br /><sub><b>Amy</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Axiaomeidan" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/kammerer"><img src="https://avatars0.githubusercontent.com/u/14025?v=4" width="100px;" alt="Tomasz Szymczyszyn"/><br /><sub><b>Tomasz Szymczyszyn</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=kammerer" title="Documentation">📖</a></td>
    <td align="center"><a href="http://nitzel.github.io/"><img src="https://avatars0.githubusercontent.com/u/8362046?v=4" width="100px;" alt="nitzel"/><br /><sub><b>nitzel</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=nitzel" title="Code">💻</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/stefanbrato"><img src="https://avatars2.githubusercontent.com/u/4852275?v=4" width="100px;" alt="dirk"/><br /><sub><b>dirk</b></sub></a><br /><a href="#ideas-stefanbrato" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/0xADD1E"><img src="https://avatars1.githubusercontent.com/u/38090404?v=4" width="100px;" alt="Addie Morrison"/><br /><sub><b>Addie Morrison</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3A0xADD1E" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://blog.alec.coffee"><img src="https://avatars2.githubusercontent.com/u/6475934?v=4" width="100px;" alt="Alec Brunelle"/><br /><sub><b>Alec Brunelle</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Aaleccool213" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://glebbahmutov.com/"><img src="https://avatars1.githubusercontent.com/u/2212006?v=4" width="100px;" alt="Gleb Bahmutov"/><br /><sub><b>Gleb Bahmutov</b></sub></a><br /><a href="#ideas-bahmutov" title="Ideas, Planning, & Feedback">🤔</a></td>
    <td align="center"><a href="https://github.com/JesseDeBruijne"><img src="https://avatars1.githubusercontent.com/u/29858373?v=4" width="100px;" alt="Jesse de Bruijne"/><br /><sub><b>Jesse de Bruijne</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=JesseDeBruijne" title="Documentation">📖</a></td>
    <td align="center"><a href="https://github.com/justinlittman"><img src="https://avatars1.githubusercontent.com/u/588335?v=4" width="100px;" alt="Justin Littman"/><br /><sub><b>Justin Littman</b></sub></a><br /><a href="#plugin-justinlittman" title="Plugin/utility libraries">🔌</a> <a href="#question-justinlittman" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://github.com/harrison9149"><img src="https://avatars0.githubusercontent.com/u/41189790?v=4" width="100px;" alt="harrison9149"/><br /><sub><b>harrison9149</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/issues?q=author%3Aharrison9149" title="Bug reports">🐛</a></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/jdcl32"><img src="https://avatars1.githubusercontent.com/u/17127746?v=4" width="100px;" alt="jdcl32"/><br /><sub><b>jdcl32</b></sub></a><br /><a href="#question-jdcl32" title="Answering Questions">💬</a></td>
    <td align="center"><a href="https://github.com/ds300"><img src="https://avatars2.githubusercontent.com/u/1242537?v=4" width="100px;" alt="David Sheldrick"/><br /><sub><b>David Sheldrick</b></sub></a><br /><a href="https://github.com/abramenal/cypress-file-upload/commits?author=ds300" title="Code">💻</a></td>
  </tr>
</table>

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

## License

[MIT][mit]

[cypress]: https://cypress.io/
[cy.fixture]: https://docs.cypress.io/api/commands/fixture.html
[cy.trigger]: https://docs.cypress.io/api/commands/trigger.html#Arguments
[npm]: https://www.npmjs.com/
[mime]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types
[mit]: https://opensource.org/licenses/MIT
[#34]: https://github.com/abramenal/cypress-file-upload/issues/34
[#41]: https://github.com/abramenal/cypress-file-upload/issues/41
[#70]: https://github.com/abramenal/cypress-file-upload/issues/70
[#74]: https://github.com/abramenal/cypress-file-upload/issues/74
[#104]: https://github.com/abramenal/cypress-file-upload/issues/104
