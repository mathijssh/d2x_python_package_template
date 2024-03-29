# dream2nix python package template (w/ optional PyCharm and direnv features)
I've created this template to create an isolated enviroment for developing python projects using Pycharm (Community Edition) from JetBrains.

### Features:
- Uses [dream2nix](https://github.com/nix-community/dream2nix), to maximize reproduciblity of python packaging
  - Based on the example in [`examples/packages/single-language/python-project`](https://github.com/nix-community/dream2nix/tree/67c1356f20b5f0495c46f1f25c45327a9e604c56/examples/packages/single-language/python-project).
  - Modified to move most parameter configuration to `pyproject.toml`
- Published as flake
- (optional, checkout branch `direnv`) Added `.envrc` to automatically load shell environment using [direnv](https://github.com/direnv/direnv/)
- (optional, checkout branch `pycharm`) Small bashscript to load PyCharm from the terminal, while suppressing stdout

### How to use:

#### Initial set-up
1. Fork this repo and `git checkout`
2. cd into the folder
3. Modify `pyproject.toml` according to your project
4. Enable environment `$ nix run --impure` to start shell environment (will build all dependencies on first run and after any updates)
5. (or, optionally, instead of step 4.) Enable direnv by running `direnv allow` and auto-enable shell environment and update
6. Update the `lock.json` by running the command generated by dream2nix (see terminal output, `bash -c /nix/...` or something similar)
7. (optionally, to use with PyCharm)
   1. (prerequisite: `pkgs.jetbrains.pycharm-community` is installed in global package space (e.g in configuration.nix or via home-manager))
   2. From the terminal with the environment active, run `where python` and copy the path to the python bin 
   3. un `$ ./pycharm.sh` (ensure it's executable by `$ chmod +x pycharm.sh`)
   4. (Close terminal, if you want)
   5. In PyCharm, add the new interpreter:
        - Settings > Add New Interpreter > Virtual Environment
        - Check **Existing** 
        - Paste the copied path from step 7.2 

### Adding packages (⚠️ cumbersome, WIP 🚧)
Currently, pycharm needs to restarted after installing new python packages. I'm looking into ways to fix this, might be (very) complicated/impossible.
1. Modify `pyproject.toml
2. Re-enable environment (see step 4/5 above)
3. Update `lock.json` (see above)
4. Save your work and close PyCharm
5. Re-run PyCharm from the terminal

Please let me know in case something is not clear, doesn't work as described or can be improved.

