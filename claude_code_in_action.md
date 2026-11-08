

# A routine can fire on a few kinds of triggers:
1. A cron schedule, like every morning at 9am.
2. An HTTP POST to its API endpoint, so your own code can kick it off.
3. A GitHub event, like a new pull request landing.

# Here's the quick decision guide:
1. Routines are the default for repeat work. They run on Anthropic's infrastructure with nothing for you to host.
2. Headless mode with -p is for when the job needs your pipeline and you want to pipe data through a script.
3. --bare is for when CI needs the same results every single run.
4. The Agent SDK is for when the work belongs inside your own product.


# Question 1: Incorrect answer

You can describe exactly what "done" looks like for a task (all tests in a package pass, the type checker reports zero errors) better than you can list the steps to get there. Which approach fits best?
Run the task in plan mode and read the plan
Use /goal to set a completion condition so Claude keeps working until a fast evaluator confirms it
Use loop to re-run the prompt on a fixed interval
Use /compact with instructions so the summary keeps what matters
Feedback:

The best fit is /goal: it sets a checkable completion condition and keeps Claude working across turns until a fast evaluator confirms it, instead of stopping the first time it thinks it is finished.

# Question 2: Incorrect answer

Your team has a hard rule: never push to main. Where should it live so Claude cannot skip it?
In the project CLAUDE.md as an "IMPORTANT" rule
In the local CLAUDE.md so it is scoped to you
In a pre-tool use hook that stops the push
In a skill's reference.md file
Feedback:

The answer is the pre-tool use hook. CLAUDE.md (project or local) is instructions Claude follows, not enforced configuration, and skills are also instructions; a hard rule belongs in a hook, which stops the action even when Claude tries it.

# Question 3: Correct answer

You have typed the same multi-step procedure to Claude more than once, and it includes long reference material and a helper script. How should you package it?
Paste the whole procedure into CLAUDE.md so it always loads
Make a skill, keep skill.md lean, and push depth into reference.md and scripts Claude runs when needed
Put every step and the full reference inline in skill.md so nothing is missed
Add it as an org-level managed policy
Feedback:

Right. A repeated procedure is a skill; the folder can hold reference files read only when needed and scripts Claude executes, so skill.md stays lean.

# Question 4: Correct answer

You ask Claude in auto mode to refactor authentication and it writes broken authentication. What actually happens, and what should you add?
The classifier blocks it because broken code is dangerous; nothing more needed
The classifier waves it through because broken is not dangerous; pair auto mode with a stop hook that runs your tests
Bypass permissions would have caught it; switch to that mode
Plan mode would have caught it; switch to that mode
Feedback:

Right. The auto-mode classifier guards intent (danger), not correctness, so it allows broken-but-safe code; a stop hook that runs tests confirms the code actually works.

# Question 5: Correct answer

You want a dependency audit to run every morning at 9am with no machine of yours staying on and no workflow file to maintain. Which tool fits?
A headless -p run you trigger manually
The Agent SDK embedded in your own application
A routine that runs on Anthropic infrastructure on a cron trigger
A bypass-permissions session left running overnight
Feedback:

Right. Routines run on a cron trigger on Anthropic infrastructure, so nothing of yours stays on and there is no workflow file to maintain.

# Question 6: Correct answer

Your team wants Claude to review every pull request with inline comments and nothing to build or host, and you do not need it to approve or block the PR. Which option fits?
The Claude Code GitHub action with a custom workflow
Managed code review through the Claude GitHub app
A headless -p run triggered by a webhook you maintain
The /code-review --fix command run locally on each PR
Feedback:

Right. Managed code review is Anthropic-hosted, posts ranked inline findings through the GitHub app, and never approves or blocks; the action is for jobs beyond review.

# Question 7: Correct answer

A job ran unattended in CI and reports success. What is the most reliable first move before you ship it?
Read Claude's summary of the run and trust the passing claim
Start from the diff itself and git diff, and confirm tests actually passed rather than were claimed
Re-run the same prompt and compare summaries
Switch the run to bypass permissions and run it again
Feedback:

Right. A tidy summary can read fine while the diff touched unexpected files; verification starts from the diff and from evidence that tests really passed, sized to how unsupervised the run was.

# Question 8: Correct answer

A community plugin gives you a skill you want. What should you do before enabling it?
Install it; plugins cannot change how Claude Code behaves by default
Install it if it passed automated review, since reviewed means trusted
Inspect every hook, agent, and MCP server it adds, because a plugin runs code with your privileges and its hooks fire on every matching call
Rely on namespacing, since a plugin cannot ship a settings.json
Feedback:

Right. A plugin runs code with your privileges and its hooks stack with yours on every matching call; reviewed is not the same as trusted, so read what it does before enabling.

Source : https://anthropic-partners.skilljar.com/claude-code-in-action/487234