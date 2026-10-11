# ai
musings about (free) ai, including my rules.md

v2026-10-11-20-23-10


 ### how to use ai for free (free trial) 

 \- the obvious ways: use web interface: claude, chatgpt, gemini, deepseek, copilot

\- less obvious: you can create 3 different mail accounts

\- free 1 month trial: if you pester chatgpt web enough, you will see button on above chat saying 'upgrade' or something similar. you get chat gpt plus, free for month. credit card mail and phone number required. you can cancel, and you will still get to use it for month (did not cancel it yet). You also get to use codex-cli, probably vs code too., with daily and weekly limits. week limits is about 482 messages ... Note when you exhaust weekly codex-cli/vs code limit, you can still use chatgpt web they dont use the same pool.

\- $300 google cloud bonus on free sign up. you have to spend it within 90 days. you can wire this to aider, and gemini AI of your choice: flash , .. openai/vertex\_ai/gemini-2.5-pro ... probably works with antigravity too. credit card required, phone number and email. (problem is right now 7/2026 google ai coding models are bad)

\- azure? probably has something similar, with bonus on free signup

\- aider can be paired with Gemini 3.1 Flash Lite 500 request per day. Other models are about 20 Requests per day (RPD) you can select it in the graph. When you exhaust one model you can switch to another, 3.5 , to 3.5 lite, to 3.1 ...

\- github copilot 50 messages MONTHLY - avoid

\- which models to use? Ask AI which model is recommended  for specific task. You don't need architect (Sol/Fable) for mundane tasks, or simple coding tasks.

\-opencode zen has some free ai agents like Muse Spark.

codex cli has some free monthly use. Terra is good for targeted review from other agents.

\-Luna (codex cli) uses really low amounts of tokens, but is a step down from terra (obviously), I suggest rather use free Muse Spark on Opencode Zen

Did not see this anywhere, so I hope it helps someone.

Claude web browse usage tracker that works with free plan too: [https://addons.mozilla.org/en-US/firefox/addon/claude-usage-tracker](https://addons.mozilla.org/en-US/firefox/addon/claude-usage-tracker)

EDIT note: claude web peak is utc 1 PM to 7 PM UTC window (which matches 5:00 AM to 11:00 AM PT), your tokens are used much faster, avoid that time.



<hr>

rules.md 

v2026-10-04-22-24-03

rules for working with ai for coding that I use short recap of rules.md:
- no coding till I say code word
- explain what this patch will do in plain English, and which files will be modifed
- no unnecessary refactoring, use smallest correct patch
- each source file is timestamped
- spec is updated after every (complete) change
- no changes between command and implementation without my explicit confirmation


- (for user) : if tight with session tokens write handoff to use in another session, or just copy paste everything after last spec update. (you can also use 'Claude Exporter' to export conversation to text)
- click above on rules.md to see/download it.
