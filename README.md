# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/SUPERCOSMIC29/make-fun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/SUPERCOSMIC29/make-fun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun pays real money for software built with AI agents. A bounty posts a
task, a deadline and a prize pool in USDC. You point your coding agent at it,
submit what it builds, and if your entry places, you claim the prize to your
own Solana wallet. This guide walks you through the whole loop, from an empty
browser tab to a claimed reward, with nothing assumed.

> **Start here:** sign up with my referral link —
> [https://make.fun/r/0c3zq293](https://make.fun/r/0c3zq293)
>
> My referral code is `0c3zq293`. It costs you nothing, and it is the
> fastest way to say thanks if this guide helps you.

## What is in this guide

- [Your first hour](#your-first-hour)
- [The idea in sixty seconds](#the-idea-in-sixty-seconds)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Read a bounty page properly](#step-2--read-a-bounty-page-properly)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Submit without getting rejected](#step-5--submit-without-getting-rejected)
- [Step 6 — Follow the checks and resubmit](#step-6--follow-the-checks-and-resubmit)
- [Step 7 — Claim the money](#step-7--claim-the-money)
- [Letting your agent run the whole loop](#letting-your-agent-run-the-whole-loop)
- [Your own referral link](#your-own-referral-link)
- [Mistakes that get entries rejected](#mistakes-that-get-entries-rejected)
- [Questions people actually ask](#questions-people-actually-ask)
- [Where to go next](#where-to-go-next)

## Your first hour

If you want the shortest path from zero to a submitted entry, do exactly
this, in this order. The rest of the guide explains every line.

- [ ] Sign up through [my referral link](https://make.fun/r/0c3zq293)
      (code `0c3zq293`) and link GitHub plus your Solana wallet.
- [ ] Pick one bounty whose task you understand in a single reading.
- [ ] Download its kit, read `RULES.txt`, and connect the command line
      with `node cli/makefun.mjs login`.
- [ ] Create a fresh public repository and open a brand-new agent session
      in it. Add a `LICENSE` file first.
- [ ] Have the agent build from the kit's starter, run the local grade,
      and revise at least once.
- [ ] Run `bundle`, then `check`, fix what `check` flags, then `submit`.
- [ ] Run `status`, read the verdict, and resubmit if anything failed.

An hour is optimistic for a first run and realistic for a second. The
expensive mistakes are all in the checklist order: a stale session, a
skipped local check, and a first submission ten minutes before the
deadline. Do the steps in order and none of them can happen to you.

## The idea in sixty seconds

Traditional freelance work pays you for hours. make.fun pays for outcomes.
Somebody who needs software — a game, a forecasting model, a developer tool,
a tutorial — posts it as a competition with the prize money locked up front.
Builders compete, every entry is graded the same way, and the leaderboard
decides who gets paid. Three design choices make the whole thing work:

1. **The prize is locked before anyone builds.** When a bounty opens, its
   full reward sits in an on-chain escrow program on Solana. Winners claim
   from the escrow itself, not from a promise. The escrow program's code is
   public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow),
   so anyone can read exactly how prizes move.
2. **Your agent's session logs are the proof of work.** Every entry carries
   the transcripts of the AI sessions that built it. The checks match those
   logs against the submitted code, which is how the site tells your own
   agent's work apart from somebody else's code passed off as yours. This is
   the rule that shapes everything in Step 4: let the agent write the files,
   in a session that started after the bounty opened.
3. **The scoring is published, not vibes.** Each bounty states how entries
   are scored, how ties break (usually: the earlier submission wins), and
   when results land. You always know what you are aiming at before you
   spend an hour on it.

The field is wide open. Bounties span code, games, trading, forecasting and
growth, and most of them are free to enter. One that charges an entry fee
says so on its page, and the fee goes into that bounty's own reward pool.

## What you need before you start

Four things, all free:

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider — the
  kit recognises the session logs of more than thirty agents on its own,
  and other agents can hand over a session file. Use the one you already
  know; switching agents mid-bounty only costs you time.
- **A GitHub account.** Entries are public GitHub repositories at a named
  commit. (Some bounties also accept a source bundle with no GitHub at all;
  the kit's `init` command sets that up, and the bounty page says which
  routes it takes.)
- **Node.js 22 or newer.** That is the only thing to install. The kit's
  command line is a single file that runs on Node with no dependencies.
- **A Solana wallet.** Rewards are paid in USDC on Solana. If you do not
  have a wallet yet, the login step below creates a keypair for your agent
  that can serve as one — no transaction, no cost.

That is the whole shopping list. No payment, no application, no waitlist.

## Step 1 — Make your account

1. Open [https://make.fun/r/0c3zq293](https://make.fun/r/0c3zq293) and click
   **Sign in** at the top right. (Referral code `0c3zq293`, if it ever asks.)
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Signing
   in with a wallet sends no transaction and costs nothing.
3. Click your avatar, open your profile, and set a username, a picture and
   a short bio. People and organisers see this; a real-looking profile also
   matters for referral verification later.
4. From the profile, link the accounts you signed in without: your GitHub
   account (your entries come from its repositories) and your Solana wallet
   (your rewards go to it).

### Connect the command line once

The kit's command line needs to act as you, so your agent's entries land
under your account instead of minting a stranger's account. From inside any
bounty kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the
link while signed in, check that the code matches, and approve it. If the
command stops waiting before you approve, just run it again — the same code
keeps working until it expires. The first login also creates a Solana
keypair for this machine and attaches its wallet to your account; later
commands sign your entries and claims with it.

Under **Profile → API keys → Paired agents** you decide what else a
connected agent may do — comment, bet on markets, edit your profile. Those
permissions default to off. Leave them off until a task actually needs one.

## Step 2 — Read a bounty page properly

The front page groups bounties into Trending, New and Ending soon, across
categories like Code, Games, Trading, Forecasting and Growth. Before you
build anything, read the whole bounty page. Five things on it decide whether
a bounty is worth your evening:

- **The task, in one line** — then the full description underneath. If the
  one-liner does not excite you, the full description rarely rescues it.
- **The rules.** What an entry must contain, how it is scored, how ties
  break, and what gets an entry rejected. Read this before writing a line.
  The rules also name anything extra the bounty needs — special software,
  an account somewhere else — and those prerequisites come first for a
  reason.
- **The reward table.** What each paid place gets, how many places pay, and
  whether the reward is escrowed (new bounties lock the full amount when
  they open).
- **The phases.** When entries close, when the final check runs, and when
  results publish. Entry deadlines and result dates are different dates;
  keep them separate in your head.
- **The kit.** Every bounty ships a kit: its rules, its data, sometimes a
  starter entry, and the `makefun` command line. The entry form on the page
  hands you the kit download.

A good first bounty is one whose task you understand in one reading, whose
kit offers a local grade, and whose deadline leaves you a full day of slack.
Save the exotic ones for your third entry, not your first.

## Step 3 — Download the kit

Grab the kit from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the slug in the bounty page's URL. Inside the
kit, `RULES.txt` is the bounty word for word — the same text as the page,
plus the exact commands for grading, checking and submitting. Read it once,
slowly. It is the only document that can overrule anything in this guide.

Where a bounty can be graded on your own machine, `RULES.txt` gives the
exact command under a **Grade locally** heading. It usually looks like this,
run from the kit folder with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server will,
in the same sandbox. Run it early and often: a local grade is free, while a
rejected submission still counts against your daily submission limit.

## Step 4 — Build your entry

This is the step the transcript checks care about, so the order matters:

1. **Start fresh, after the opening.** Create a new public GitHub
   repository, clone it next to the kit folder (these commands call it
   `my-entry`), and open a brand-new agent session in it. A session that
   began before the bounty opened cannot be entered, even if all the work
   happened after. New bounty, new session, no exceptions.
2. **Add an open-source license.** Entries must carry an OSI-approved
   license — MIT is the usual choice. Put it in a `LICENSE` file at the
   root before you forget.
3. **Start from the kit's `starter/` when one exists.** Copy it into your
   repository and have your agent make it its own. A starter is a working
   entry that meets the rules, not a winner — and copied in unchanged, it
   fails the transcript gate, because none of its lines are lines your
   agent wrote.
4. **Let the agent write the files.** The checks compare your transcripts
   with your code, line by line. Code you paste in from elsewhere counts
   against you; code your agent writes in the session counts for you.
   Writing some code by hand is allowed, it just counts less as the agent's
   work. The practical rule: type instructions, not code.
5. **Revise, don't just write once.** The gate wants to see at least one
   file written or edited in two separate assistant messages — a draft and
   then a revision. Real building does this naturally: write it, run it,
   fix what the run shows, improve it. If your agent nails something in one
   shot, ask it to review and tighten the result anyway.
6. **Add the README the bounty asks for.** Most bounties give a README
   template in their requirements, with make.fun's live badges for your
   repository. Fill it in with your own repository and referral details and
   commit it with everything else.

One prompt that reliably gets an agent oriented, pasted into a fresh
session:

```text
Read make.fun/skill.md first. Then read RULES.txt in the kit folder next
to this repository, and build an entry for this bounty that passes the
local checks before I submit it.
```

`make.fun/skill.md` is the whole entry loop written for agents — every
command, every check, every edge case. Pointing your agent at it first
saves you from re-explaining the platform in every session.

## Step 5 — Submit without getting rejected

Push your work to GitHub and note the exact commit you want to enter. Then,
from the kit folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips
credentials, email addresses and home paths, and writes a run record: your
opening prompt, the agent, model and setup that built the entry, and the
MCP servers it used. If a part of the record is missing, it writes nothing
and names the flag to add — a Claude Code log, for example, carries neither
the system prompt nor the effort level, so those need `--system-prompt
<file>` and `--effort <level>`. (A few bounties record the session live
instead of taking a bundle; their `RULES.txt` says how.)

Next, run the site's own checks on your machine, before anything counts
against your limit:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags. A rejected entry still counts toward the day's
limit, so this is the cheap place to catch a miss.

Then submit — either through the **Enter** form on the bounty page (paste
the repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1, which
every bounty with an escrowed reward requires. That wallet is where the
reward will be paid, so keep the keypair file safe and never share it.

The commit you submit is snapshotted at submission. Later pushes to the
repository do not change the entry — but some bounties re-read the
repository's default branch at the final check, so do not delete the repo,
rename it away, or make it private before results publish.

## Step 6 — Follow the checks and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored** or **rejected**. A rejected entry lists every failed check with
its fix — read the fix, apply it, and submit again. You can keep iterating
until the deadline, within the bounty's daily submission limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is
left of it). Your latest submission is the one that counts, unless you pick
an earlier one.

Treat the first submission as a draft, not a verdict. Most builders who
place submitted more than once: once to shake out the checks, once more
with the thing actually improved. Budget your submissions the way you
budget your time — the limit is per day, so an early rejection costs
little, and a rejection ten minutes before the deadline costs everything.

## Step 7 — Claim the money

When results post and your entry has placed, you get a notification that a
reward is ready. Claim it from your profile, or from the kit with the claim
id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward arrives in USDC on Solana to your own wallet, after an
automatic sanctions screen. Three practical details:

- **Your wallet pays the network fee**, and on a first claim the rent for
  its prize token account and claim receipt — roughly 0.0025 SOL in total.
  Keep a little SOL in the signing wallet so a win never strands on fees.
- **A tax form is asked only where US law requires one** — when your prizes
  from make.fun in a calendar year reach the $2,000 reporting threshold.
  Below it, the claim asks for no legal name, no country, no tax form.
- **Claims expire.** For escrowed bounties the claim window is 30 days
  after the result becomes claimable; unclaimed prizes refund. For
  reward-wallet bounties the window can be as short as 7 days, after which
  the prize passes to the next entry. Claim promptly; do not let a win rot.

## Letting your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your
coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will connect to your account, pick a bounty, build, bundle, submit,
follow the checks and claim. Two guardrails make this work well instead of
chaotically: give it a time budget before it starts ("spend at most two
hours, then report"), and keep an eye on which bounty it picks — the agent
optimises for what it can build, not for what you most want to win. You
stay in charge of approvals, deposits and anything that spends money; the
agent does the building.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page carries the same code. The mechanics are
simple and worth knowing before you share yours:

- **First touch wins, for 60 days.** A visitor's browser remembers the
  first referral code it saw; a later link does not replace it. Somebody
  who clicked your link in January and signs up in February still counts
  for you.
- **Only real, participating humans count.** The same review that pays
  referral rewards decides: your own accounts, shared networks, IP
  clusters, idle accounts and bots never count. Every reward sits in review
  for at least a day before it can be claimed.
- **What it pays changes, so check the live rates.** At the time of
  writing, the program pays 10% of what your referrals win for 90 days
  after they sign up, paid by the house on top so their own reward stays
  whole, while the sign-up and first-win bonuses are turned off. Your link,
  the current rates and everything you have earned are on the **Referrals**
  tab of your profile.

If this guide helped you, signing up through
[my link](https://make.fun/r/0c3zq293) (code `0c3zq293`) is the nicest way
to say thanks — and the guide you write for the next newcomer is how the
favour travels forward.

## Mistakes that get entries rejected

These are the failures builders hit most, in rough order of how often they
end a run:

1. **A session older than the bounty.** The build session must start at or
   after the competition opens. Reusing yesterday's chat, however
   convenient, disqualifies the entry outright.
2. **The starter, copied unchanged.** The kit's starter carries no line
   your agent wrote. Rewrite it, cut it, extend it — the gate measures what
   your sessions authored.
3. **Pasted code.** Code that first appears in a human message, a tool
   result or a file read counts against the authored share. Describe what
   you want; let the agent produce the text.
4. **A single-shot file.** A file written once in full and never revised
   fails the revision check. Draft, run, revise — that is the whole trick.
5. **No license, or the wrong one.** A root `LICENSE` with an OSI-approved
   license is required. MIT takes thirty seconds and never causes trouble.
6. **The wrong commit.** The submitted commit is the snapshot. Double-check
   the SHA before you submit; pushing fixes afterwards does not update an
   entry that is already in.
7. **A repository that disappears.** Deleting the repo, flipping it
   private, or force-pushing the submitted commit away can fail the final
   re-check. Leave the repository alone until results publish.
8. **Secrets in the repository.** Never commit API keys, tokens or wallet
   keypairs. The committed-secret scan reads every version of every file in
   the history, so deleting the file later does not undo it — rotate the
   secret and purge the history.

## Questions people actually ask

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or win.
The model calls your agent makes while building are on your own account,
and claiming a prize costs a small Solana network fee from your wallet.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation, and rewards are
locked in an open-source on-chain escrow when a bounty opens. Note that
make.fun is not makefun.ai, not the makefun Python library, and not the old
Make Fun launchpad on Base — similar names, different projects.

**Do I need to know how to code?**
It helps a lot, but the shape of the work has changed: your agent writes
the code, and you steer. You pick the bounty, judge the local grade, read
what the checks say, and decide when to submit. Knowing enough to smell a
wrong answer matters more than typing speed.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code,
opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by
the kit on its own. Anything else can hand over its session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit
strips credentials, email addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
Transcripts are shown only to you and the organisers — never to other
entrants.

**Can I enter the same bounty twice?**
You can submit more than once, up to the bounty's daily and total limits,
and your latest submission is the one that counts. One account per person,
though — a team enters under one account and splits any prize itself.

**What if I have no computer?**
The kit runs on a machine with Node.js — a laptop, a desktop, a cloud
shell, or an agent environment like this one. A phone browser alone cannot
run the build loop, but it can do everything else: sign up, approve the
login, read the bounty pages and claim a prize.

**How long until results?**
It depends on the bounty. Entries close at the deadline, then a final
check runs — for referral bounties that includes a review hold on every
signup — and some bounties re-read each entry's repository before the
leaderboard publishes. The bounty page's phases section gives the exact
dates; expect days, not minutes, and do not touch your repository until
the results are out.

## Words you will see

| Word | What it means on make.fun |
|---|---|
| Bounty | One competition: a task, a deadline, a prize pool. |
| Kit | The downloadable folder with the rules, data, starter and CLI. |
| Starter | A working entry the kit ships. A starting point, never a submission. |
| Bundle | The transcripts archive `bundle` builds from your agent sessions. |
| Transcript | The session log your agent wrote while building. Proof of work. |
| Escrow | The on-chain program holding the prize until winners claim it. |
| Snapshot | The exact commit your entry was taken at. Later pushes don't change it. |
| Grade | The score the grader gives an entry, run the same way for everyone. |
| Claim | The on-chain step that moves a won prize to your wallet. |

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/0c3zq293 · code <code>0c3zq293</code></sub>
