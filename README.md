# demo for https://github.com/mwouts/jupytext/issues/900

to reproduce the bug:

- setup:
  - create a virtualenv
  - install `requirements.txt`
  - install pre-commit and run `pre-commit install` (or, you can just run `jupytext` on the command line manually)
- reproduce:
  - run `jupyter-lab`
  - open `jupy_test.ipynb`, make a change, and save. 
    - this should auto-update `jupy_test.py`.
    - `git diff` should show that `jupyt_test.ipynb` now has a `metadata.jupytext` section.
  - (via pre-commit) `git commit -a -m 'test'` triggers `jupytext`. this removes the newly added `metadata.jupytext` section, causing pre-commit to fail. running `git commit -a` again succeeds.
  - (via jupytext manually) run `jupytext --sync jupy_test.ipynb` and note that the `metadata.jupytext` section was removed from the notebook
