# Designers' fork

This repository is `widelab-co/wideset-design`, the designers' fork of Wideset. Before changing any
file, opening a PR or answering a review, load the `wideset-design-lab` skill and follow it.

For the designer's workflow, this rule and that skill take precedence over `AGENTS.md`: pushing
`design/*` branches and opening PRs in this fork is part of the job, and the branches carry no
changeset, playground refresh or spec change. `develop` changes only through
`gh repo sync widelab-co/wideset-design --branch develop`, never with `--force`. Never use
`--no-verify`, even when a hook's message suggests it.
