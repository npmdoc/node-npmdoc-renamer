# api documentation for  [renamer (v0.6.1)](https://github.com/75lb/renamer#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-renamer.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-renamer) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-renamer.svg)](https://travis-ci.org/npmdoc/node-npmdoc-renamer)
#### Batch rename files and folders

[![NPM](https://nodei.co/npm/renamer.png?downloads=true)](https://www.npmjs.com/package/renamer)

[![apidoc](https://npmdoc.github.io/node-npmdoc-renamer/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-renamer_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-renamer/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-renamer/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-renamer/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Lloyd Brookes"
    },
    "bin": {
        "renamer": "bin/cli.js"
    },
    "bugs": {
        "url": "https://github.com/75lb/renamer/issues"
    },
    "dependencies": {
        "app-usage-stats": "^0.4.0",
        "array-back": "^1.0.3",
        "command-line-tool": "^0.6.4",
        "console-dope": "~0.3.6",
        "file-set": "^1.1.1",
        "string-tools": "^1.0.0",
        "test-value": "^2.1.0"
    },
    "description": "Batch rename files and folders",
    "devDependencies": {
        "core-assert": "^0.2.1",
        "more-fs": "~0.5.0",
        "test-runner": "^0.3.0"
    },
    "directories": {},
    "dist": {
        "shasum": "66293ae2c622def4071e50af8a137df509ffcc8c",
        "tarball": "https://registry.npmjs.org/renamer/-/renamer-0.6.1.tgz"
    },
    "gitHead": "33e9c75d2c75475178818151acd2eba06069d45f",
    "homepage": "https://github.com/75lb/renamer#readme",
    "license": "MIT",
    "main": "./lib/renamer",
    "maintainers": [
        {
            "name": "75lb",
            "email": "75pound@gmail.com"
        }
    ],
    "name": "renamer",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/75lb/renamer.git"
    },
    "scripts": {
        "test": "test-runner test/cli.js test/renamer.*.js"
    },
    "version": "0.6.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module renamer](#apidoc.module.renamer)
1.  [function <span class="apidocSignatureSpan">renamer.</span>Result (options)](#apidoc.element.renamer.Result)
1.  [function <span class="apidocSignatureSpan">renamer.</span>Results (list)](#apidoc.element.renamer.Results)
1.  [function <span class="apidocSignatureSpan">renamer.</span>dryRun (results)](#apidoc.element.renamer.dryRun)
1.  [function <span class="apidocSignatureSpan">renamer.</span>expand (files)](#apidoc.element.renamer.expand)
1.  [function <span class="apidocSignatureSpan">renamer.</span>rename (results)](#apidoc.element.renamer.rename)
1.  [function <span class="apidocSignatureSpan">renamer.</span>replace (options)](#apidoc.element.renamer.replace)
1.  [function <span class="apidocSignatureSpan">renamer.</span>replaceIndexToken (results)](#apidoc.element.renamer.replaceIndexToken)



# <a name="apidoc.module.renamer"></a>[module renamer](#apidoc.module.renamer)

#### <a name="apidoc.element.renamer.Result"></a>[function <span class="apidocSignatureSpan">renamer.</span>Result (options)](#apidoc.element.renamer.Result)
- description and source-code
```javascript
function Result(options) {
  if (options.before) this.before = options.before
  if (options.after) this.after = options.after
  if (options.renamed) this.renamed = options.renamed
  if (options.error) this.error = options.error
  if (options.stat) this.stat = options.stat
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.Results"></a>[function <span class="apidocSignatureSpan">renamer.</span>Results (list)](#apidoc.element.renamer.Results)
- description and source-code
```javascript
function Results(list) {
  this.list = list || []
  this.add = function (files) {
    var self = this
    arrayify(files).forEach(function (file) {
      if (!testValue(self.list, { before: file })) {
        self.list.push({ before: file })
      }
    })
  }
  this.beforeList = function () {
    return this.list.map(function (item) {
      return item.before
    })
  }
  this.afterList = function () {
    return pluck(this.list, 'after', 'before')
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.dryRun"></a>[function <span class="apidocSignatureSpan">renamer.</span>dryRun (results)](#apidoc.element.renamer.dryRun)
- description and source-code
```javascript
function dryRun(results) {
  results.list = results.list.map(function (result, index, resultsSoFar) {
    var existing = resultsSoFar.filter(function (prevResult, prevIndex) {
      return prevIndex < index && (prevResult.before !== result.before) && (prevResult.after === result.after)
    })

    if (result.before === result.after || !result.after) {
      result.renamed = false
      result.error = 'no change'
    } else if (existing.length) {
      result.renamed = false
      result.error = 'file exists'
    } else {
      result.renamed = true
    }

    return result
  })
  return results
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.expand"></a>[function <span class="apidocSignatureSpan">renamer.</span>expand (files)](#apidoc.element.renamer.expand)
- description and source-code
```javascript
function expand(files) {
  var fileStats = fileSet(files)
  fileStats.filesAndDirs = fileStats.files.concat(fileStats.dirs.reverse())
  return fileStats
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.rename"></a>[function <span class="apidocSignatureSpan">renamer.</span>rename (results)](#apidoc.element.renamer.rename)
- description and source-code
```javascript
function rename(results) {
  results.list = results.list.map(function (result) {
    if (!result.after) {
      result.renamed = false
      result.error = 'no change'
      return result
    }
    try {
      if (fs.existsSync(result.after)) {
        result.renamed = false
        result.error = 'file exists'
      } else {
        fs.renameSync(result.before, result.after)
        result.renamed = true
      }
    } catch (e) {
      result.renamed = false
      result.error = e.message
    }
    return result
  })
  return results
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.replace"></a>[function <span class="apidocSignatureSpan">renamer.</span>replace (options)](#apidoc.element.renamer.replace)
- description and source-code
```javascript
function replace(options) {
  var metrics = { invocation: 1 }
  for (var option in options) {
    metrics[option] = 1
  }
  usage.hit({ name: 'replace' }, metrics)
  var findRegex = regExBuilder(options)
  var results = new Results()
  results.list = options.files.map(replaceSingle.bind(null, findRegex, options.replace))
  return results
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.renamer.replaceIndexToken"></a>[function <span class="apidocSignatureSpan">renamer.</span>replaceIndexToken (results)](#apidoc.element.renamer.replaceIndexToken)
- description and source-code
```javascript
function replaceIndexToken(results) {
  results.list = results.list.map(function (result, index) {
    if (result.after) {
      result.after = result.after.replace('{{index}}', index + 1)
    }
    return result
  })
  return results
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
