# Faith Hope Love Token — a beginner's guide

Welcome. This repository contains a very small **smart-contract** experiment called
`FaithHopeLoveToken`. You do not need to understand it all at once. Programming is
not a test of how much you can memorize; it is the practical habit of turning a
small, clear idea into instructions, checking the result, and improving it.

> **Important:** This is a learning project, not financial, legal, or security
> advice. Do not put real money into a token project or share a wallet's secret
> recovery phrase/private key with anyone (including an AI). A smart contract can
> be expensive or impossible to change after it is published.

## 1. What you are looking at

There are only two project files today:

| File | In everyday words |
| --- | --- |
| [`FaithHopeLoveToken`](./FaithHopeLoveToken) | The recipe for a digital token. It is written in a language named Solidity. |
| `README.md` | This guide—the human-friendly explanation of the project. |

Think of a program as a recipe:

1. **Input:** someone asks it to do something.
2. **Rules:** the program follows the exact steps written by its author.
3. **Output:** it records or returns a result.

For a token, the result is a record of who owns how many units. A smart contract is
that recipe stored on a blockchain: many computers keep matching copies of the
record and follow the same rules. Publishing a contract is called **deploying** it.

## 2. The token's story, from beginning to end

The file `FaithHopeLoveToken` describes this simple sequence:

1. A person deploys the contract.
2. During deployment, its `constructor` runs once.
3. The constructor creates 100 whole FHLT tokens and gives them to the deployer's
   wallet address.
4. After that, the standard token rules allow holders to check balances and send
   tokens using the functions supplied by OpenZeppelin, a widely used collection of
   prebuilt code.

The contract says the full name is **FaithHopeLoveToken** and its short label is
**FHLT**. Computers store a whole token as many tiny units, in the same way that a
dollar is stored as cents. This contract uses the standard 18 tiny-unit places, so
the code creates `100 × 10¹⁸` tiny units, displayed to people as 100 tokens.

That is all this version does. It **does not** promise a price, create a website,
find buyers, guarantee safety, or make a token valuable. Code can define rules; it
cannot create trust or demand by itself.

## 3. Reading the contract without panic

Open [`FaithHopeLoveToken`](./FaithHopeLoveToken) and read it top to bottom. Here
is a translation of each part:

```solidity
// SPDX-License-Identifier: MIT
```

This labels the permission terms for the code. It is like a label explaining how
others may use the recipe.

```solidity
pragma solidity ^0.8.10;
```

This asks for Solidity version 0.8.10 or a later compatible 0.8 version. A
**programming language** is simply a carefully defined way to write instructions
for computers.

```solidity
import ".../ERC20.sol";
```

This brings in an ERC-20 implementation. **ERC-20** is a common shared agreement
for how a token should behave—for example, how to ask for a balance or transfer
tokens. Reusing trusted, reviewed building blocks is safer than re-writing basic
rules yourself, but it is still essential to review and test the whole result.

```solidity
contract FaithHopeLoveToken is ERC20 {
```

This starts our token's recipe. The words `is ERC20` mean “start with the usual
ERC-20 behavior, then add our own setup instructions.”

```solidity
constructor() ERC20("FaithHopeLoveToken", "FHLT") {
```

The **constructor** is the one-time setup step that runs on deployment. It gives
the base ERC-20 contract the token's name and short label.

```solidity
_mint(msg.sender, 100 * 10**uint(decimals()));
```

`_mint` creates token units. `msg.sender` means “the wallet that started this
action”; for deployment, that is the deployer. `decimals()` is 18 here. The leading
underscore in `_mint` signals an internal helper: users cannot call it directly.

## 4. How to think like a programmer

Do not begin by trying to write lots of code. Start by making the next small fact
clear.

### A repeatable problem-solving loop

1. **State the goal in one sentence.** Example: “The token should initially give
   100 tokens to the deployer.”
2. **List examples.** “If Alice deploys it, Alice starts with 100. Bob starts with
   0.” Examples make vague wishes testable.
3. **Break it into tiny steps.** Name the token; create the amount; assign it to
   the deployer.
4. **Change one small thing.** Avoid changing ten things at once.
5. **Run a check.** Compile the code or run an automated test.
6. **Read the result.** An error message is a clue, not a verdict about you.
7. **Explain what happened in plain words.** If you cannot explain it yet, ask for
   an explanation or make the experiment smaller.
8. **Keep the working change.** Save it with a short note using Git (explained
   below).

When something breaks, use this template before guessing:

```text
Goal: I expected ...
What I did: I changed/run ...
What happened: I saw ...
Smallest next experiment: I will try ...
```

This is the central skill. Experts are not people who never see errors; they are
people who turn errors into small, checkable questions.

## 5. Your first safe coding session

For a first experiment, use a browser-based Solidity learning environment such as
Remix **only with its simulated JavaScript VM**, not a real wallet or real network.
The exact buttons may change, so ask Codex to describe the current screen if you
need help.

1. Open Remix and make a new file named `FaithHopeLoveToken.sol`.
2. Copy the contents of this repository's `FaithHopeLoveToken` file into it.
3. Compile it. **Compile** means checking that the recipe is valid Solidity and
   translating it into a form the blockchain can use. Do not worry about every
   warning; read one message at a time.
4. Select the simulated JavaScript VM and deploy the contract there. This is a
   pretend blockchain inside the tool, so it does not spend real cryptocurrency.
5. Click `balanceOf`, paste the simulated deployer address, and read the result.
   It may show `100000000000000000000`—the tiny units described above.
6. Switch to another simulated address. Check its balance (zero), then use
   `transfer` to send one token from the deployer account. Check both balances.

Pause after each step and predict the result before clicking. A prediction makes
learning active: if the result differs, you have found exactly what to investigate.

## 6. Using Codex well

Codex is an assistant that can read project files, propose and make changes, run
checks, and explain the work. Treat it like a fast collaborator, not an authority.
It can be wrong, misunderstand your goal, or make a change that works technically
but is not what you wanted.

### A strong request has five parts

1. **Starting point:** “I am a beginner. Explain every new word.”
2. **Outcome:** “Add a fixed supply of 1,000 practice tokens.”
3. **Limits:** “Do not deploy anything; do not use a wallet; change only this
   file.”
4. **Proof:** “Run the available checks and tell me exactly what passed or failed.”
5. **Teaching:** “Show the before/after difference and explain why each line
   changed.”

Copy and adapt this prompt:

```text
I am learning and want to make one small, safe change.
First, inspect this repository and explain its files in everyday language.
Then propose a plan; do not change anything until I say yes.
When I approve, change only [FILE] to [GOAL].
Explain each changed line, define unfamiliar terms, run the relevant checks,
and clearly separate facts from guesses. Do not deploy, publish, or use funds.
```

### Good questions to ask Codex

- “Explain this line as if I have never programmed. Then give one tiny example.”
- “What could go wrong if I make this change? Rank the risks from most serious.”
- “Write a test for the behavior I described before writing the contract change.”
- “Show me the exact change before applying it.”
- “I got this error. Explain the first likely cause and one safe next step:
  `[paste the full error]`.”
- “Quiz me with three questions about this file. Wait for my answer after each.”

### Questions to avoid

- “Make my token successful.” Success is not a precise code requirement.
- “Make it secure” without saying what it should do. Ask for a threat review,
  tests, and an explanation of remaining risks instead.
- “Deploy it everywhere.” Deployment can spend money and has real consequences.
- “Fix everything.” Ask for the smallest reproducible problem and a plan.

### Always review before trusting a change

Ask Codex to show: what files changed, what behavior changed, what was checked,
and what was **not** checked. Read the change slowly. For money-related smart
contracts, get an experienced independent security review before any real use.

Never paste these into a prompt, code file, screenshot, or chat:

- wallet recovery phrase (often 12 or 24 words);
- private key;
- passwords or API keys;
- personal data you do not want shared.

## 7. Saving work with Git, in plain language

Git is a history book for a project. A **commit** is one saved snapshot with a
short explanation. A **branch** is a separate line of experiments, so you can try
something without mixing it into another piece of work. A **pull request** is a
request to review and merge a branch's changes.

For learning projects, a healthy rhythm is:

1. Make one small change.
2. Run a check.
3. Read the list of changes.
4. Commit only when you can explain what changed.

Useful commands—type them in the project folder, one at a time:

```bash
git status                 # What has changed?
git diff                   # What exactly changed?
git log --oneline -5       # What are the last five saved snapshots?
git add README.md          # Select this file for the next snapshot
git commit -m "Explain token setup"  # Save with a meaningful note
```

Do not run a command just because someone says to. Ask what it will do first.
Commands beginning with `rm`, `git reset --hard`, or `git push --force` can remove
work or overwrite shared history; stop and understand them before using them.

## 8. A gentle learning path

Move on only when the previous step feels mostly comfortable. It is normal to
repeat a step many times.

1. **Weeks 1–2: basic programming.** Learn variables (named boxes for values),
   decisions (`if`), repetition (loops), functions (named reusable steps), and
   tests (small programs that verify expectations). Use a beginner-friendly general
   language such as Python or JavaScript before focusing on blockchain code.
2. **Weeks 3–4: web and Git basics.** Make a tiny page, learn how files relate,
   use commits, and practise reading errors.
3. **Weeks 5–6: Solidity foundations.** Learn wallet addresses, numbers, mappings
   (a lookup table, such as address → balance), functions, and events (recorded
   notices that apps can listen for).
4. **Weeks 7–8: testing and security thinking.** Write expected examples, test
   both normal and invalid actions, and ask “who is allowed to do this?” for every
   function that changes data.
5. **Afterward: small projects.** Build a practice token on a simulation, then a
   simple non-financial contract. Keep real money out of the learning loop.

## 9. Next exercises for this repository

Do these one at a time. Before changing code, write down what should happen.

1. Change only the **name** and **symbol** in a copy of the contract. Compile it
   and observe that the initial balance is still 100.
2. Change the initial supply from 100 to 250. Predict the tiny-unit value first,
   then confirm it in a simulated environment.
3. Write a short test plan in this README: deployer balance, another address's
   balance, and a transfer between them.
4. Ask Codex to help turn that plan into automated tests, explaining every line.
5. Ask Codex for a security review of the *specific* behavior, then compare its
   concerns with the contract's actual capabilities.

Do not add features such as public minting, fees, blacklists, owner controls, or
pausing merely because they sound useful. Each rule changes who has power and can
introduce bugs or trust problems. First write the human rule, its examples, and
who should be allowed to use it.

## 10. The most important habit

Your goal is not to understand every technical detail today. Your goal is to make
one safe, observable change at a time and learn from the result. Whenever you are
unsure, ask: **“What does this do, how can I check it, and what is the safest
smallest next step?”**
