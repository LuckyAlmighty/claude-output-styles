Claude Code output style(s) for engineers who want the answer first, in plain English, with every technical detail intact.

## Why

I tried almost every output style I could find.

* **Claude's built-ins:** Default, Concise, Explanatory, Learning.
* **Community styles:** No Slop, No AI Slop (after Peter Yang), ADHD, STE-BLUF-ACE, Yoda, and a few more.

None of them fit how I read.

* Default explains too much and closes with offers I never asked for.
* Concise cuts so hard that conditions and numbers disappear.
* The opinionated styles read well, but they rewrite qualifiers and round things off.
* Strict simplified-English styles are precise but tiring to read.

I wanted three things together:

* Short, plain sentences I understand on the first read.
* Related facts grouped, with details nested under them.
* Code, commands, numbers, and conditions kept byte-for-byte exact.

So I wrote my own. It borrows the discipline of ASD-STE100 Simplified Technical English and adds hierarchical bullets and strict technical-detail preservation.

## Example

Question: *Why does my API call fail after the token refresh?*

**Default style**

> Great question! The issue you're seeing is most likely caused by the retry logic. When the request times out, the client retries, but it's worth noting that the token was already refreshed in the meantime, which means the second request goes out with a stale token. To fix this, you'll want to read the token inside the interceptor rather than capturing it when the interceptor is created. I hope this helps! Let me know if you have any other questions.

**Plain Concise**

> * The retry sends a stale token.
>
>   * The interceptor captures the token when it is created.
>   * A refresh replaces the token, but the retry still uses the captured value.
> * Fix: read the token inside the interceptor on each request.
> * Verify: let the token expire, send a request, and confirm the retry returns `200`.

Same facts, fewer words, no preamble, no closer, and the verification step is explicit.

## What the style does

* Leads with the result. No "Sure", "Let me", or "I'll".
* Uses short sentences, active voice, and common words.
* Groups related facts under one bullet and nests the details.
* Numbers only the steps where order matters.
* Keeps code, commands, paths, identifiers, numbers, and conditions exact.

  * "Only after a restart" never becomes "Always".
  * "For files larger than 10 MB" never becomes "For large files".
* Never claims something is fixed or verified without evidence.

  * It says "Implemented. Tests were not run." instead of "Should be working."
* No em dashes, no filler, no marketing language.

## Install

1. Copy the style into your user output-styles folder:

   ```bash
   mkdir -p ~/.claude/output-styles
   curl -fsSL https://raw.githubusercontent.com/LuckyAlmighty/claude-output-styles/main/plain-concise.md \
     -o ~/.claude/output-styles/plain-concise.md
   ```

   For one project only, put it in `.claude/output-styles/` inside that repo instead.

2. In Claude Code, select it:

   ```text
   /output-style Plain Concise
   ```

   If Claude Code says the style is unknown, run `/output-style` once with no arguments to reload the list, then try again.

## Credits

* ASD-STE100 Simplified Technical English for the writing discipline.

## License

MIT
