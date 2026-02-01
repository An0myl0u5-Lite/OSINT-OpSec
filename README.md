# OSINT-OpSec
compilation of tools and advice for OSINT and OpSec 

GitHub Malware Honeytrap Repositories: Full Breakdown
The Big Picture
There are five distinct but interconnected campaigns that have been discovered, researched, and publicly reported. This is well-documented, widely known in the security community, and still an active threat.

CAMPAIGN 1: Stargazers Ghost Network (The Foundation)
Discovered by: Check Point Research
Published: July 24, 2024
Threat Actor: Tracked as "Stargazer Goblin"

WHO
Unknown operator(s) running a Distribution-as-a-Service (DaaS) business
Sells GitHub manipulation services to other criminals on dark web forums
Pricing: $10 to star 100 accounts, $2 for an "aged" repository with history
WHAT
A network of 3,000+ ghost accounts on GitHub
Accounts are segmented by role: some star repos, some host phishing templates, some host malicious releases
This segmentation means GitHub can only kill part of the network at a time
Automated recovery system detects banned accounts and replaces them
WHEN
Development/testing began August 2022
Scaled operations through 2023
Major Atlantida Stealer campaign: January 2024 (1,300+ victims in 4 days)
Check Point published findings: July 2024
Still active with 200+ repos as of mid-2024 despite takedowns
WHERE
Primarily GitHub, but similar ghost accounts across YouTube, Discord, Instagram, X (Twitter), Facebook
Cross-platform amplification to drive traffic to malicious repos
WHY
Revenue: estimated $100,000 total, ~$8,000 in a single month
Business model: other criminals pay Stargazer Goblin to distribute their malware
HOW
Fake stars, forks, watchers inflate repository credibility
Repos target people looking for: social media follower tools, cracked software, crypto tools
Malware delivered: Atlantida Stealer, Rhadamanthys, RisePro, Lumma Stealer, RedLine
GITHUB RESPONSE
Removed ~1,559 repositories and associated accounts since May 2024
200+ remained active at time of Check Point's report
No public statement from GitHub naming the network specifically
LAW ENFORCEMENT
No arrests or indictments reported for the operators behind this network
CAMPAIGN 2: PyStoreRAT - Fake OSINT & GPT Tools (Directly Relevant to You)
Discovered by: Morphisec Threat Labs (researcher Yonatan Edri)
Published: December 11, 2025
Attribution: Unknown; Russian-language artifacts ("СИСТЕМА" = "SYSTEM") found in codebase, suggesting Eastern European origin

WHO
Unknown threat actor(s), likely Eastern European
Used techniques "reminiscent of" the Stargazers Ghost Network (may be customers or copycats)
WHAT
Fake GitHub repos masquerading as:
OSINT tools (e.g., "OSINT360-GPT")
GPT/AI chat wrappers
DeFi/crypto trading bots
Security utilities
Deployed a previously unknown RAT called PyStoreRAT
WHEN
Earliest activity: mid-June 2025
Steady stream of new repos published through summer
Malicious "maintenance" commits injected: October-November 2025
Reported: December 2025
HOW (The Trap - This Is The Clever Part)
Create new or reactivate dormant GitHub accounts
Publish polished, AI-generated projects that look legitimate
Promote via YouTube and X/Twitter
Artificially inflate stars and forks
Several repos climbed onto GitHub's trending lists
Wait for trust to build
Push subtle "maintenance" commits containing the backdoor
Many tools displayed only static menus or non-interactive UIs - they never actually worked
PyStoreRAT CAPABILITIES
Modular, multi-stage implant
Executes: EXE, DLL, PowerShell, MSI, Python, JavaScript, HTA modules
Deploys Rhadamanthys infostealer as follow-on payload
Targets crypto wallets: Ledger Live, Trezor, Exodus, Atomic, Guarda, BitBox02
Encrypted C2 communications
Persistence via scheduled task disguised as "NVIDIA App SelfUpdate" (runs every 10 minutes)
Spreads via USB/removable media using malicious LNK files
Rotating C2 infrastructure using GitHub-hosted nodes and disposable domains
TARGETS
Security researchers
OSINT analysts
Cryptocurrency users
Developers
IOCs AVAILABLE
Full IOC list, YARA rules, and GitHub cluster correlations in Morphisec's downloadable report
Hackread published repo names with screenshots
Symantec (Broadcom) published detection bulletin December 18, 2025
CAMPAIGN 3: Webrat - Fake CVE Exploit PoCs
Discovered by: Kaspersky (Solar 4RAYS team initially, October 2025)
Published: December 23, 2025
Attribution: Unknown

WHO
Unknown threat actor targeting junior security researchers and infosec students
WHAT
15 malicious repositories hosting fake proof-of-concept exploits for real high-profile CVEs
Distributed Webrat (WebRAT) backdoor
WHEN
Active since at least September 2025
Kaspersky discovered in October 2025
Published December 23, 2025
HOW
Repos named after real CVEs with high CVSS scores:
CVE-2025-59295 (IE heap overflow, CVSS 8.8)
CVE-2025-10294 (WordPress auth bypass, CVSS 9.8)
CVE-2025-59230 (Windows Remote Access, CVSS 7.8)
AI-generated READMEs with detailed technical write-ups
Password-protected ZIP with password hidden in filename
Inside: decoy DLL + batch file + main executable (rasmanesc.exe)
KNOWN MALICIOUS ACCOUNTS (now removed)
RedFoxNxploits/CVE-2025-10294-Poc
FixingPhantom/CVE-2025-10294
h4xnz/CVE-2025-10294-POC
usjnx72726w/CVE-2025-59295
11+ more (15 total)
WEBRAT CAPABILITIES
Steals credentials from: Steam, Discord, Telegram
Steals crypto wallet data
Webcam and screen surveillance
Keylogging
Disables Windows Defender
Privilege escalation
STATUS
All 15 repos removed by GitHub
Prior victims still at risk until manually cleaned
CAMPAIGN 4: Banana Squad - Trojanized Hacking Tools
Discovered by: ReversingLabs
Published: June 2025
Threat Actor: "Banana Squad" (named after their domain bananasquad[.]ru)

WHO
First spotted by Checkmarx in October 2023
Original campaign started April 2023
Russian infrastructure (bananasquad[.]ru, 1312services[.]ru, 1312stealer[.]ru)
WHAT
200+ trojanized repositories (67 initially identified, more found later)
Impersonated legitimate hacking tools: credential stealers, vulnerability scanners, Discord account cleaners
HOW (Stealth Technique - Very Clever)
Exploited GitHub's UI: long strings of spaces push malicious code off-screen to the right
In normal GitHub view, code looks clean - the backdoor is hidden past the horizontal scroll
Repo names identical to real, legitimate repos (typosquatting)
"About" sections packed with SEO keywords and flame/rocket emojis (AI-generated)
Automated GitHub Actions workflows simulated active development
PAYLOADS
4 backdoor types embedded in:
Visual Studio PreBuild events (111 repos)
Python scripts
Screensaver files
JavaScript (17,000 lines of obfuscated code in an Electron app)
Final payloads: AsyncRAT, Remcos RAT, Lumma Stealer
Disables Windows Defender, deletes shadow copies
STATUS
All 67 identified repos removed by GitHub
Unknown number of victims (clone counts not public)
CAMPAIGN 5: AI-Assisted Fake Repos (SmartLoader/Lumma)
Discovered by: Trend Micro
Published: March 2025
Related: Microsoft also tracked a parallel malvertising campaign (Dec 2024 - Jan 2025, ~1 million devices affected)

WHAT
Fake repos disguised as gaming cheats, cracked software, system tools
Distributed SmartLoader which delivered Lumma Stealer
AI-generated README files as primary lure
Malicious files stored in GitHub Releases section
SUMMARY: WHAT'S KNOWN AND WHAT ISN'T
Question	Answer
Is it known/reported?	Yes. Extensively. Check Point, Morphisec, Kaspersky, ReversingLabs, Trend Micro, Microsoft, and dozens of outlets have covered it.
Who is behind it?	Stargazer Goblin (DaaS operator) is the infrastructure. Individual campaigns have separate operators. Russian-language artifacts found in PyStoreRAT. Banana Squad uses .ru domains. No individual identities publicly known.
Arrests?	None reported for any of these campaigns specifically. Related law enforcement has hit Lumma Stealer infrastructure (DOJ/Europol/Microsoft joint operation, 2025) but not the GitHub distribution layer.
GitHub's response?	Reactive takedowns: 1,559+ repos from Ghost Network, 67+ from Banana Squad, 15 from Webrat, unknown number from PyStoreRAT. No proactive detection system publicly announced.
Still active?	Yes. Researchers warn that new repos continue to appear. The automated recovery systems mean takedowns are temporary setbacks.
AI involvement?	Heavy. AI generates READMEs, commit histories, code structure, and promotional content. Check Point warns AI-driven ghost accounts are the next evolution.
RED FLAGS TO WATCH FOR
If you're evaluating any OSINT repo, look for:

Account age vs. repo quality - brand new account with polished project
Star/fork ratio looks unnatural - many stars, few real issues/PRs
AI-generated READMEs - overly polished, generic language, flame/rocket emojis
Password-protected ZIPs in releases
Tools that don't actually work - static menus, placeholder outputs
"Maintenance" commits that add obfuscated code months after initial publication
No real community - no discussions, no issue responses, no contributor history
Horizontal scrolling hides code (Banana Squad technique)
Sources
Check Point Research - Stargazers Ghost Network
Morphisec - PyStoreRAT Campaign
The Hacker News - PyStoreRAT
Hackread - PyStoreRAT Repo List
Kaspersky Securelist - Webrat
BleepingComputer - Webrat
ReversingLabs - Banana Squad
The Hacker News - Banana Squad
Trend Micro - AI-Assisted Fake Repos
Microsoft - Malvertising via GitHub
IBM - 3000 Ghost Accounts
SecurityWeek - 3000 GitHub Accounts
Infosecurity Magazine - Banana Squad
CSO Online - Webrat
