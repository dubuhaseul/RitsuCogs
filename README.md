# RitsuCogs

Some Unix/Linux and Anime related cogs for <a href="https://github.com/Twentysix26/Red-DiscordBot">Red-DiscordBot</a>. If you need help or want to chat, visit my <a href="https://discord.gg/25w9hKX">Discord channel</a>.

Add repo: ```[p]cog repo add ritsu-cogs https://github.com/ritsu/RitsuCogs```

## GNU

An attempt to emulate some common GNU utilities. 

### Pipes

Output from one command can be piped to the input of another.

```[p]sed "s/^.{0,20}$//" http://news.google.com | grep -i apple | sed s/apple/Orange/i | tail -n 5```

Prefix is optional for commands that appear after a pipe. 

### Input and Output

All commands accept input from the following:

- Website content if a valid URL is specified
- Chat log if @chat is specified (Chat log must be enabled for the channel, e.g. `!clog on`)
- Any text following the command if none of the above are detected.

The following options for input and output apply to all non-administrative commands:

```
Global Options
    -p       If input is a URL, this will treat the URL content as (prettified) html instead of a DOM.
    -@       Same as -p except source is not passed through BeautifulSoup's prettify().
    -%       Print each line as a separate message; more likely to hit Discord's 5/5 rate limit.
```

Chat log options can be configured with the <b>clog</b> command.

### Redirected output

Output can be redirected to <a href="http://pastebin.com/">pastebin</a> instead of Discord chat with the syntax `> paste_title`. If successful, a link to the generated pastebin will be posted in chat. When used with pipes, the redirect must appear at the end.

```[p]cat http://news.google.com > latest_news```

A <a href="http://pastebin.com/api">pastebin API key</a> is required for this feature. Save the API key with the command:

```[p]pastebin [api_key]```

### grep

<i>grep</i> prints lines that contain a match for a pattern.

```grep [options] [pattern] [input]```
```
Matching Options
    -i       Ignore case distinctions, so that characters that differ only in case match each other.
    -w       Select only those lines containing matches that form whole words.
    -v       Invert the sense of matching, to select non-matching lines.
    -r       Treats search string as a regex pattern; other Matching Options are ignored.

Output Options
    -c       Suppress normal output; instead print a count of matching lines for each input file.
    -n       Prefix each line of output with its line number.
    -m num   Stop reading from input after num matching lines.
    -A num   Print num lines of trailing context after matching lines.
    -B num   Print num lines of leading context before matching lines.
    -C num   Print num lines of leading and trailing context.
```

### sed

<i>sed</i> is a simple stream editor.

```sed [options] [script] [input]```
```
Options
    -g       Process entire input as a single string, rather than line by line.
    -n       Disable automatic printing; only produce output when explicitly told to.

Script Address
    /.../    Returns lines that match the regular expression.
    A        Returns line number A.
    A,B      Returns lines from A to B.
    A~N      Returns every Nth line, starting from A

Script Command
    a...     Append after each line.
    c...     Change lines with new line.
    d        Delete lines.
    i...     Insert before each line.
    p        Print line.
    s/././   Substitute with regular expression pattern.
    =        Print line number.

Script Pattern Flag
    /i       Ignore case
    /p       Print (mostly used when -n option is active)
```

### wc

<i>wc</i> counts the number of characters, whitespace-separated words, and newlines in the given input.

```wc [option] [input]```
```
Options
    -m      Print only the character counts.
    -w      Print only the word counts.
    -l      Print only the newline counts.
```

### cat

<i>cat</i> echoes the contents of the input.

```cat [options] [input]```
```
Options
    -b      Number all nonempty output lines, starting with 1.
    -n      Number all output lines, starting with 1. This option is ignored if -b is in effect.
    -s      Suppress repeated adjacent blank lines; output just one empty line instead of several.
```

### tac

<i>tac</i> echoes input to output in reverse by line or user specified separator.

```tac [options] [input]```
```
Options
    -s sep  Use "sep" as the record separator, instead of newline.
    -r      Treat the separator string as a regular expression.
```

### tail

<i>tail</i> prints the last part (10 lines by default) of input.

```tail [options] [input]```
```
Options
    -n [+]num   Output the last num lines. However, if num is prefixed with a '+'
                start printing with line num from the start of input, instead of from the end.
```

## TokyoTosho

### Get search results in your discord channel

`[p]tt search [terms] [#type]`

<b>terms</b> are normal searech terms. Prepend a "-" for exclusion terms.  
<b>type</b> (optional) is one of the types/categories defined on TokyoTosho. Type `[p]tt types` to see a list of valid types.

Example: `!tt search madoka rebellion -dub #anime`

### Show RSS alerts in your discord channel

`[p]tt add [terms] [#types]`

Adds an alert to your channel. The bot will display torrent name and link when a new torrent matching the configured <b>terms</b> and <b>types</b> (optional) appears in TokyoTosho's RSS feed. Note you can specify multiple types for RSS alerts.

Example: `!tt add shokugeki 1080 -raw #anime`

### Manage RSS alerts

`[p]tt list`

Lists existing alerts configured for your channel.

`[p]tt check`

Checks existing alerts against the current RSS feed. The latest (1) item will be returned for each alert. The RSS feed only contains the last 150 items, so old items will not appear.

`[p]tt remove [terms] [#types]`

Removes alerts matching (exactly) the specified <b>terms</b> and <b>types</b> if they exist in your channel. If no matching alerts are found, nothing happens.

### Config options

`[p]tt set [option] [value]`

Sets various options

- `check_interval` Number of seconds between RSS updates
- `comment_length` Max length of search result and RSS feed comments
- `ignore` List of categories that are ignored in all search and RSS alerts
- `items_per_message` Max number of items the bot will mention in one message

