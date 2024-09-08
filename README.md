This repo was created in order to demonstrate an issue with pants resolve system where `pytest` is located in the lockfile yet is unrecognized when running tests.


## Steps to reproduce

### 1. Generate lockfiles

```sh
$ pants generate-lockfiles --generate-lockfiles-resolve=pants-plugins
```

`pants-plugins/lock.json` contains `pytest`:

```sh
$ grep 'pytest<7' lock.json
"pytest<7.1.0,>=6.2.4" 
```

### 2. Run tests

```sh
$ pants test ::
...
[WARN] Pants cannot infer owners for the following imports in the target pants-plugins/myplugin/test.py:

  * pytest (line: 1)

If you do not expect an import to be inferrable, add `# pants: no-infer-dep` to the import line. Otherwise, see https://www.pantsbuild.org/2.21/docs/using-pants/troubleshooting-common-issues#import-errors-and-missing-dependencies for common problems.
...
```

