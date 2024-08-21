> [!NOTE]
> This git repo is using a franken-repo approach,
> submodules are actually stored in this very same git repo!

Versions:
* `chuffed`: `0.13.2` (`2016f7eb7943a86b9ce93bb70b821d701667a5ca`)
* `gecode`: `release/6.3.0` branch commit (`f7f0d7c273d6844698f01cec8229ebe0b66a016a`, aka `release-6.2.0-204-gf7f0d7c27`)
* `libminizinc`: `2.8.5` (`2fdef7b40921981f3f9ea82017e9d84937ddab77`)
* `minizinc-python`: `0.9.0` (`3fc2ffc7c7f85326f3cca1da2a07151a8f4c0a68`)
* `pytest-html`: `4.1.1` (`cfd32d08488e2c6fb72f0617db94ab41d3fca8d0`)

Usage workflow:
```
git clone minizinc-meta
cd minizinc-meta
git config --local protocol.file.allow always
git submodule init
git submodule sync
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
git -c protocol.file.allow=always submodule update --reference ./
git submodule foreach 'git config --local protocol.file.allow always'
```

Adding `libminizinc` submodule/subproject:
```
git remote add libminizinc https://github.com/MiniZinc/libminizinc.git
git fetch --all --prune
git tag libminizinc/2.8.5 2fdef7b40921981f3f9ea82017e9d84937ddab77
git -c protocol.file.allow=always submodule add --name libminizinc --reference ./ -- ./ libminizinc
git submodule sync
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
cd libminizinc && git checkout -f libminizinc/2.8.5 && cd ..
```

Adding `minizinc-python` submodule/subproject:
```
git remote add minizinc-python https://github.com/MiniZinc/minizinc-python.git
git fetch --all --prune
git tag minizinc-python/0.9.0 3fc2ffc7c7f85326f3cca1da2a07151a8f4c0a68
git -c protocol.file.allow=always submodule add --name minizinc-python --reference ./ -- ./ minizinc-python
git submodule sync
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
cd minizinc-python && git checkout -f minizinc-python/0.9.0 && cd ..
```

Adding `pytest-html` submodule/subproject:
```
git remote add pytest-html https://github.com/pytest-dev/pytest-html.git
git fetch --all --prune
git tag pytest-html/4.1.1 cfd32d08488e2c6fb72f0617db94ab41d3fca8d0
git -c protocol.file.allow=always submodule add --name pytest-html --reference ./ -- ./ pytest-html
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
git -c protocol.file.allow=always submodule update --reference ./
git submodule foreach 'git config --local protocol.file.allow always'
cd pytest-html && git checkout -f pytest-html/4.1.1 && cd ..
```

Adding `chuffed` submodule/subproject:
```
git remote add chuffed https://github.com/chuffed/chuffed.git
git fetch --all --prune
git tag chuffed/0.13.2 2016f7eb7943a86b9ce93bb70b821d701667a5ca
git -c protocol.file.allow=always submodule add --name chuffed --reference ./ -- ./ chuffed
git submodule sync
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
cd chuffed && git checkout -f chuffed/0.13.2 && cd ..
```

Adding `gecode` submodule/subproject:
```
git remote add gecode https://github.com/Gecode/gecode.git
git fetch --all --prune
git tag gecode/6.2.0+20240315150732+git204+gf7f0d7c27 f7f0d7c273d6844698f01cec8229ebe0b66a016a
git -c protocol.file.allow=always submodule add --name gecode --reference ./ -- ./ gecode
git submodule sync
git submodule foreach 'cd .. && git submodule set-url $sm_path `pwd`'
cd gecode && git checkout -f gecode/6.2.0+20240315150732+git204+gf7f0d7c27 && cd ..
```

`git format-patch -p gecode/6.2.0+20240315150732+git204+gf7f0d7c27..gecode/pq --src-prefix=a/gecode/ --dst-prefix=b/gecode/ --output-directory=../debian/patches/gecode/`
`git format-patch -p libminizinc/2.8.5..libminizinc/pq --src-prefix=a/libminizinc/ --dst-prefix=b/libminizinc/ --output-directory=../debian/patches/libminizinc/`
`git format-patch -p minizinc-python/0.9.0..minizinc-python/pq --src-prefix=a/minizinc-python/ --dst-prefix=b/minizinc-python/ --output-directory=../debian/patches/minizinc-python/`
`git format-patch -p pytest-html/4.1.1..pytest-html/pq --src-prefix=a/pytest-html/ --dst-prefix=b/pytest-html/ --output-directory=../debian/patches/pytest-html/`
`git diff -p -U99999 0.13.2 --src-prefix=a/chuffed/ --dst-prefix=b/chuffed/ > ../debian/patches/0001-chuffed-fix-cmake.patch`
