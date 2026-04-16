---
title: Installing humanizer library
created: 2026-03-15T22:06:22.007116Z
updated: 2026-03-17T20:30:52.151977Z
uuid: cf00708e-8af1-4b8e-820f-c9049fa63ffb
source: claude-conversation
type: source
message_count: 22
---

# Installing humanizer library

## Phelipe

lets install this
https://github.com/blader/humanizer

---

## Claude

Let me check what this is first.
```
This block is not supported on your current device yet.
```

Good find. 8.5k stars, MIT license, based on Wikipedia's AI writing detection patterns. It's basically a checklist of 24 AI-isms (significance inflation, em dash overuse, sycophantic tone, etc.) packaged as a Claude Code skill. Aligns well with your existing brand rules, which already ban most of the same things.

You already have a lot of these patterns prohibited in your Loud Hawk BRAND.md and COCKPIT instructions. This skill would formalize them as a reusable pass you can run on any draft.

To install in Claude Code, run this in Warp:

```bash
mkdir -p ~/.claude/skills/humanizer
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer
```

Then you can invoke it with `/humanizer` or just ask Claude Code to humanize a draft. Worth running on Loud Hawk Edition 2 and the email sequence before they ship.

One thing to watch: the skill will flag em dashes, which you already ban. It won't know your specific brand voice rules (the Loud Hawk register, the OSA Connect tone). So treat it as a cleanup pass, not a voice pass. Your BRAND.md files are still the voice authority.

Want me to also draft an update to your INSTALLED-PLUGINS.md and SKILLS-STACK.md to log this addition?

---

## Phelipe

yes

---

## Claude

Let me read the current files first.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now I'll create the updated versions of both files.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Both files updated. Changes:

**INSTALLED-PLUGINS.md:** Bumped totals to 21 plugins / 36 commands. Added "Manual Installs" section with humanizer. Fixed the truncated command list at the bottom (added `/humanizer` and the missing marketing line).

**SKILLS-STACK.md:** Added humanizer as entry #6 in Tier 2 (renumbered everything below). Moved it into Phase 2 (Marketing & Content) in the install priority order with a ✅. Added it to the layer diagram as "Content Cleanup layer."

Drop these into `~/Desktop/OSA/connect/skills/` to replace the originals. Then run the git clone in Warp to actually install.

---

## Phelipe

its in doawloads. just give me command

---

## Claude

```bash
cp ~/Downloads/INSTALLED-PLUGINS.md ~/Downloads/SKILLS-STACK.md ~/Desktop/OSA/connect/skills/
```

---

## Phelipe

sorry is in download on this file

---

## Claude

Looks like they landed in a `files (1)` subfolder inside Downloads. Try:

```bash
cp ~/Downloads/files\ \(1\)/INSTALLED-PLUGINS.md ~/Downloads/files\ \(1\)/SKILLS-STACK.md ~/Desktop/OSA/connect/skills/
```

---

## Phelipe

done

---

## Claude

Good. Now install the actual skill in Warp:

```bash
mkdir -p ~/.claude/skills/humanizer && git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer
```

After that, you can test it on Edition 2 before it ships on the 26th.

---

## Claude

All done. Humanizer is installed, docs are updated, plugins confirmed globally. 

What's next?

---

## Phelipe

add humanizer here

---

## Claude

That's the Claude.ai Skills panel, not Claude Code. Different system. The humanizer you just installed lives in `~/.claude/skills/` and works in Claude Code via Warp.

To add it here in Claude.ai, hit the **+** button at the top of the Skills sidebar, then paste the contents of the SKILL.md file from the repo. You can grab it with:

```bash
cat ~/.claude/skills/humanizer/SKILL.md | pbcopy
```

That copies it to your clipboard. Then in Claude.ai: **+** → give it the name "humanizer" → paste the content → save.

---

## Claude

It wants an .md file upload. In Warp, open Finder to that file:

```bash
open ~/.claude/skills/humanizer/SKILL.md
```

Then drag that SKILL.md file into the upload dialog. Or just navigate to `~/.claude/skills/humanizer/` in Finder (Cmd+Shift+G, paste the path) and drag it in.

---

## Phelipe

cd ~/Desktop/OSA/connect && claude --dangerously-skip-permissions
 ▐▛███▜▌   Claude Code v2.1.76
▝▜█████▛▘  Sonnet 4.6 · Claude Pro
  ▘▘ ▝▝    ~/Desktop/OSA/connect
❯ /ralph-loop:help                                                                   
  ⎿  Interrupted · What should Claude do instead?
❯ /plugin list                                                                       
  ⎿  (no content)
❯ /plugin marketplace add Owl-Listener/designer-skills                               
  ⎿  Successfully added marketplace: designer-skills
❯ /plugin install designer-skills                                                    
  ⎿  Plugin "designer-skills" not found in any marketplace
                                                                                     
❯ /plugin install ui-design@designer-skills                                          
  ⎿  Plugin 'ui-design@designer-skills' is already installed globally. Use '/plugin'
     to manage existing plugins.                                                     
                                                                                   
❯ /plugin install design-research@designer-skills                                    
  ⎿  Plugin 'design-research@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ /plugin install design-systems@designer-skills                                     
  ⎿  Plugin 'design-systems@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ /plugin install ux-strategy@designer-skills                                        
  ⎿  Plugin 'ux-strategy@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ /plugin install interaction-design@designer-skills                                 
  ⎿  Plugin 'interaction-design@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ /plugin install prototyping-testing@designer-skills                                
  ⎿  Plugin 'prototyping-testing@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ /plugin install design-ops@designer-skills                                         
  ⎿  Plugin 'design-ops@designer-skills' is already installed globally. Use '/plugin'
      to manage existing plugins.                                                    
                                                                                   
❯ /plugin install designer-toolkit@designer-skills                                   
  ⎿  Plugin 'designer-toolkit@designer-skills' is already installed globally. Use
     '/plugin' to manage existing plugins.                                           
                                                                                   
❯ mkdir -p ~/.claude/skills/humanizer                                                
git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer         
                                                                                     
⏺ It looks like you want to set up a humanizer skill. Shall I run those commands for 
  you?                                                                               
                                                                                     
  mkdir -p ~/.claude/skills/humanizer                                                
  git clone https://github.com/blader/humanizer.git ~/.claude/skills/humanizer       
                                                                                     
❯ cp ~/Downloads/INSTALLED-PLUGINS.md ~/Downloads/SKILLS-STACK.md                    
~/Desktop/OSA/connect/skills/                                                        
                                                                                     
⏺ Bash(cp ~/Downloads/INSTALLED-PLUGINS.md ~/Downloads/SKILLS-STACK.md               
      /Users/phelipehonesto/Desktop/OSA/connect/skills/)                             
  ⎿  Error: Exit code 1                                                              
     cp: /Users/phelipehonesto/Downloads/INSTALLED-PLUGINS.md: No such file or 
     directory                                                                       
     cp: /Users/phelipehonesto/Downloads/SKILLS-STACK.md: No such file or directory
                                                                                     
⏺ Those files don't exist at ~/Downloads/. Could you check the filenames or location?
                                                                                     
❯ cp ~/Downloads/files\ \(1\)/INSTALLED-PLUGINS.md ~/Downloads/files\                
\(1\)/SKILLS-STACK.md ~/Desktop/OSA/connect/skills/                                  
                                                                                     
⏺ Bash(cp ~/Downloads/files\ \(1\)/INSTALLED-PLUGINS.md ~/Downloads/files\           
      \(1\)/SKILLS-STACK.md /Users/phelipehonesto/Desktop/OSA/connect/skills/)       
  ⎿  Done                                                                            
   
⏺ Done.                                                                              
                                                                  
❯ mkdir -p ~/.claude/skills/humanizer && git clone                                   
https://github.com/blader/humanizer.git ~/.claude/skills/humanizer                   
                                                                                     
⏺ Bash(mkdir -p ~/.claude/skills/humanizer && git clone                              
      https://github.com/blader/humanizer.git ~/.claude/skills/humanizer)            
  ⎿  Cloning into '/Users/phelipehonesto/.claude/skills/humanizer'...                
   
⏺ Done. Humanizer skill cloned to ~/.claude/skills/humanizer.                        
                                                                  
❯ open ~/.claude/skills/humanizer/SKILL.md                                           
                                           
⏺ Read 1 file (ctrl+o to expand)                                                     
                                                                  
⏺ The humanizer skill is a thorough writing editor that removes AI patterns from     
  text. Key capabilities:                                                            
                                                                                     
  - 24 AI writing patterns it detects and fixes (em dashes, rule of three, vague     
  attributions, promotional language, AI vocabulary words, etc.)                     
  - Personality injection — not just removing bad patterns but adding voice, rhythm, 
  and specificity                                                 
  - Two-pass process — draft rewrite, then a self-audit ("what makes this obviously
  AI?"), then final revision
  It's now installed at ~/.claude/skills/humanizer/ and registered as the humanizer
  skill. You can invoke it with /humanizer on any text you want de-AI'd.
─────────────────────────────────────────────────────────────────────────────────────
❯  
─────────────────────────────────────────────────────────────────────────────────────
  ⏵⏵ bypass permissions on (shift+tab to cycle)

---

## Claude

Claude Code read the file instead of opening it in Finder. Run this instead:

```bash
open -R ~/.claude/skills/humanizer/SKILL.md
```

That opens Finder with the file selected. Then drag it into the Claude.ai upload dialog.

---

## Claude

Live in both places now. Claude Code and Claude.ai. You're set.

---

## Phelipe

did we build linked in skills ?

---

## Claude

No. You have the Marketing Skills plugin from coreyhaines31 installed, which covers general social media and copywriting. But nothing specific to LinkedIn content creation, posting cadence, or the 4 posts/week strategy from your launch checklist.

Worth building? Your checklist says "LinkedIn outreach: 4 posts/week per your locked content strategy." A dedicated skill could codify your voice rules, post formats, and the OSA/Loud Hawk content mix so Claude Code generates on-brand LinkedIn drafts consistently.
```
This block is not supported on your current device yet.
```

---
