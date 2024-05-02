# tp-lab04
Study of continuous integration systems on the example of Travis CI service.

## Tutorial

```sh
❯ export GITHUB_USERNAME=TheIIIrd
❯ export GITHUB_TOKEN=e0208e19e7eed790c91a47d69940be5c401c4a058417f1564c74e8baf6bc74f7
```

```sh
❯ cd ${GITHUB_USERNAME}/workspace
❯ pushd .
~/TheIIIrd/workspace ~/TheIIIrd/workspace

❯ source scripts/activate
```

```sh
❯ git clone git@github.com:${GITHUB_USERNAME}/tp-lab03.git projects/lab04
Cloning into 'projects/lab04'...
remote: Enumerating objects: 28, done.
remote: Counting objects: 100% (28/28), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 28 (delta 7), reused 24 (delta 6), pack-reused 0
Receiving objects: 100% (28/28), 21.99 KiB | 21.99 MiB/s, done.
Resolving deltas: 100% (7/7), done.

❯ cd projects/lab04
❯ git remote remove origin
❯ git remote add origin git@github.com:${GITHUB_USERNAME}/tp-lab04.git
```

```sh
❯ cat > .travis.yml <<EOF
language: cpp
EOF

❯ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF

❯ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```sh
❯ git add .travis.yml
                                                                                        
❯ git commit -m "added CI"
[main 9320fc2] added CI
 1 file changed, 14 insertions(+)
 create mode 100644 .travis.yml
                                                                                        
❯ git push origin main
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 442 bytes | 442.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:TheIIIrd/tp-lab04.git
   c7458b7..9320fc2  main -> main
```
