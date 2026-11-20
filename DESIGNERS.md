# Working in the designers' fork

`widelab-co/wideset-design` is a copy of [Wideset](https://github.com/widelab-co/wideset) for
design work with an AI agent. You change styles, motion, stories and docs here, as many pull
requests as you like and of any size. Nothing is merged in this fork: the dev team ports your
finished pull requests to Wideset.

## Set up once

You need Git, the GitHub CLI (`gh`) and Node 22 with pnpm (see the Wideset
[README](README.md) for versions).

```bash
gh auth login -s workflow        # already logged in? gh auth refresh -s workflow
gh repo clone widelab-co/wideset-design
cd wideset-design
pnpm install                     # also installs the Git hooks
```

The `workflow` scope lets your agent update the fork when Wideset changes its CI files. Without
it, the session start fails with a message about the `workflow` scope.

## Start a session

Open your agent in the `wideset-design` folder and start with the design skill:

- **Claude Code:** it loads the fork's rules by itself. Say what you want to change, or type
  `/wideset-design-lab` first.
- **Codex:** start your first message with `$wideset-design-lab`.
- **Other agents:** ask the agent to read `.agents/skills/wideset-design-lab/SKILL.md` and follow
  it.

The agent updates the fork from Wideset, asks which topic you are working on, and keeps one
branch and one pull request per topic. Run `pnpm storybook` to see your changes at
http://localhost:6006.

Tell the agent what you want in design terms ("the active tab should slide, as in this Figma
frame") and paste Figma links. Things it cannot do in a visual change, such as a new prop or a
missing token, it writes in the pull request as `OPEN:` items for the dev team.

## Your pull request

1. The agent opens it as a draft and keeps its description up to date: why, Figma link,
   Storybook story, what changed. Drag before/after screenshots into its table on GitHub.
2. When you are done, tell the agent. It marks the pull request ready, adds the `ready-for-port`
   label and asks CodeRabbit for a review, then goes through CodeRabbit's comments with you.
   From then on the branch only takes fixes from review; new work is a new topic.
3. The dev team takes it from there:
   - `porting`: a developer is moving it to Wideset in their own pull request(s);
   - `ported`: it is in Wideset; the pull request here is closed with links;
   - `declined`: not moved, with the reason in a comment;
   - `needs-design`: something needs a change in Figma first (for example a missing token).

If the agent says the fork or a branch needs a developer (a sync conflict), ask in the team
channel. Never merge a pull request in this fork, even though GitHub offers the button.
