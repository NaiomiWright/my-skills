# My Claude Code skills

Three Claude Code skills I wrote for my own marketing work.

By Naiomi Wright, brand and product marketer in animal health. See [naiomiwright.com](https://naiomiwright.com).

A skill is a short set of instructions that Claude Code follows when you ask for a task. Each one is a single `SKILL.md` file.

## The skills

### campaign-kit

- **What it does:** turns a short brief for any product into a full campaign kit: the Excel plan, the external pack, the internal pack, a landing page with tracked links, and a results dashboard once there are results.
- **Where it came from:** one real week of work on my [Marketing Lab](https://github.com/NaiomiWright/marketing-lab) portfolio project, a made-up campaign for a made-up dog chew. [Read the case study](https://naiomiwright.github.io/marketing-lab/case-study/).
- **What makes it different:** it includes what went wrong that week and how each problem was fixed, so the same mistakes do not happen twice.
- **Built-in checks:** no medical claims, every total is a formula, nothing is invented, and nothing is published without asking.
- **Tested:** on a second made-up product, a joint supplement for older cats. It built the plan and three emails in about four and a half minutes.
- **Note:** it builds Office files with Microsoft Office on Windows, so it needs Excel, Word and PowerPoint installed.

### tracked-link

- **What it does:** builds a tracked link (a page address with UTM tags on the end), so you can see which post, email or advert brought people to a page.
- **You give it:** the page address, the channel, the type of item and the campaign name.
- **It gives you:** one clean link, with tags in lower case and hyphens in place of spaces.
- **Why it matters:** every link in a campaign follows the same pattern, so the results are easy to read.

### my-launch-email

- **What it does:** writes a launch email in my own voice, to my team, my company or customers.
- **How it works:** it reads my private voice profile on my own computer, asks who the email is for and the one thing they must do, then follows my launch email rules.
- **Built-in checks:** no medical claims, one clear ask, and it never sends anything.
- **It learns:** if I say a draft does not sound like me, it adds my correction as a new rule.
- **Note:** my voice profile is private, so it is not in this repository. The skill stops if the profile is missing.

## How to install

1. Install [Claude Code](https://claude.com/claude-code).
2. Download this repository. Click the green **Code** button, then **Download ZIP**, and unzip it.
3. Copy the folders inside `skills` into your own skills folder:
   - Windows: `C:\Users\<your name>\.claude\skills\`
   - Mac: `~/.claude/skills/`
4. Restart Claude Code. Type `/campaign-kit`, `/tracked-link` or `/my-launch-email` to use them.

Or, with Git:

```
git clone https://github.com/NaiomiWright/my-skills.git
```

Then copy the three folders from `my-skills/skills` into your skills folder, as in step 3.
