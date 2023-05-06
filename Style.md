# Documentation style and formatting

## English style

Write short sentences. Organize concepts in paragraphs. Prefer lists to tables and paragraphs to lists. Write in the active voice. Avoid jargon beyond the requirements of subject and audience.

### Eschew you

You write unambiguous documentation, so you avoid the second person. Avoiding personal pronouns in general helps produce the imperative impersonal tone desired for documentation. Don't reboot your system or have the user reboot their system. Reboot the system.

### Generalities

There are a few other common ways to write or not write things:

* The first word of a sentence is always capitalized.
* Expand acronyms on their introduction in a document, with the short form following in parentheses: Trusted Platform Module (TPM).
* Terms of art that are not commands or other literal text should often be italicized on their first appearance in a document: *Kubernetes* is a good example.
* There is one space (` `) after a period (aka *full stop*, `.`), comma (`,`), semicolon (`;`) and other marks of punctuation.


#### Project names are (mostly) proper nouns

Project may not not capitalized, except when appearing as the first word of a sentence. Examples: etcd or rkt. It is contextual so be a little observant.

The capitalization rules are traditional and arcane. They should eventually give way to all project and product names being capitalized as proper nouns, except when given literally, e.g., `rkt run docker://nginx` or `/var/lib/rkt`.

## Unix style: Command line grammar

*Commands* *invoke* or *execute* programs. Commands *take* *arguments* and *accept* *options*, which themselves may be *set* to *values*.

### Example: Documenting `echo(1)`

In this simple command line:

```sh
$ echo -n Example
Example
```

`echo` is the command, and `Example` is the argument. The option `-n` suppresses the terminating newline usually emitted by `echo`. A binary option represented by a single letter, like `-n`, is sometimes called a *flag*. The `echo(1)` command prints its argument on the standard output, and a good shell excerpt often includes the expected output of commands, as shown here. The shell prompt character `$` distinguishes input from output.

### Example: Documenting subcommands

Some command lines are more complex. Many commands operate through a set of *subcommands*. `rkt` and several other relevant programs follow this pattern.

```sh
$ rkt run --debug example.aci
[...]
```

In this case the argument to `rkt`, `run`, is a subcommand. `run` in turn accepts the `--debug` option to modify how it executes the ACI image specified by its own argument, `example.aci`

### Example: Documenting long command lines

Some commands pack many subcommands, arguments, and options on a single line. It is good practice to break such long command lines with newlines, escaped with backslash (`\`), because lines inside code blocks are not soft-wrapped in most presentations. For very long command lines, choose points that break the parameters into logical groups. Lines so wrapped are not indented for vertical alignment.

```sh
$ docker run --name container \
-i -t \
-p 80:80 -p 443:9443 \
-v /etc/ssl/certs:/etc/ssl/certs \
image
```

### Comment conventions

Add comments inline if possible, and before the referenced line of code if not.

```yaml
staticPasswords:
- email: "admin@example.com"
  # bcrypt hash of the string "password".
  hash: "$2a$10$2b2cU8CPhOTaGrs1HRQuAueS7JTT5ZHsHSzYiFPm1leZck7Mc8T4W"
  username: "admin" # username to display. NOT used during login.
  userID: "08a8684b-db88-4b73-90a9-3cd1661f5466"
```

### Placeholder conventions

Use these standard example entities to avoid exposing real URLs, IP Addresses, or other data.

* URL: [example.com][rfc2606s3]
* IP Address: [Any in the range 203.0.113.0/24][rfc5737]

## Source formatting

Satyarat documentation is written in [Markdown][mdhome], a simple way to annotate text to indicate presentation typesetting. Markdown source is intended to be a plain text human-readable version of the document, even before conversion to HTML for the browser or other display.

### Source file naming and encoding

Write Markdown source in UTF-encoded plain text files, named with a reasonable, lower case short form of the document's title, and suffixed with `.md`. Prefer hyphens to underscores in file names with two or more words. For example, instructions for DNS configuration are written to a file named *configuring-dns.md*.

### Line wrapping considered harmful

Don't wrap long lines of text with manual newlines. Line wrapping churns prose documents, because lines not actually edited will nevertheless change when a paragraph is edited and rewrapped.

### One sentence per line deprecated

Do not add a line break between sentences. Write natural English paragraphs, separated by a single blank line. Writing Markdown source with a newline between every sentence is acceptable to most compilers and can ease change review. However, this format makes the document less readable in source form.

### Preferred markdown symbols

Markdown defines two or more ways to declare some document structures. This documentation prefers these Markdown symbols among their alternatives:

* Headings are denoted in Markdown's ATX style, with hash character(s): `#`. See [*Headings*][headings], below.
* Bulleted lists, like this one, are denoted with the asterisk (`*`), rather than the hyphen.
* Hyperlink URLs are given in the reference style (`[hyperlinked text][label]`), rather than inline. Hyperlink labels are defined in one list at the end of the document. Relative links are preferred to absolute links. See [*Hyperlink Considerations*][hyperlink-considerations], below.
* *Italic text* is wrapped with a pair of single asterisks: `*Italics*`; **Bold** with a double pair: `**Bold**`.
* `Monospace` is indicated between a pair of backticks. This distinguishes literal strings like command names, file paths, or values, e.g., `/bin/markdown`. See [*Command Line Grammar*][command-line-grammar], below.
* Longer code blocks or file contents are *fenced*: Set off on new lines between pairs of three backticks, rather than indented. A presentation hint specifying the block's language can be given immediately after the opening three backticks, e.g., ````yaml`.

## Headings

By convention, the level one heading, denoted in Markdown by a single hash character (`#`), is the document's title. This document's title is *Documentation style and formatting*.

### Heading style

Each heading is both preceded and followed by a newline. A space separates the Markdown symbols from the heading text. Headings are typed in *Sentence case*, capitalizing the first letter of the first word, but other words only as they would be capitalized if appearing in the middle of a sentence.

### Heading semantics and the sidebar outline

Section headings expose the document's logical structure with a notation of incrementing hash marks (`#[#][...]`) for increasingly nested levels of a hierarchy. With the level one heading devoted to the document title, the second-level headings represent the document's primary concepts.

### Example: The "average" document

Most documents have a single `h1` (`#`) heading matching the title, two to five `h2` (`##`) headings representing the topic's primary concepts, and one or two `h3` (`###`) and `h4` (`####`) headings organizing details beneath each `h2`.

If a document proves a great deal longer or more structurally complex than those simplistic rules of thumb, there should be a good reason.

## Hyperlink considerations

### Naming

Name hyperlinks carefully to give them maximum context. For example, note that certain information is in the [style guide][style], rather than just pointing lazily to the style guide [here][style]. The link text "here" gives almost no information about its target. It is helpful to [write a clear sentence][eos] first, then bracket the choice words within to declare them a hyperlink.

### Marking down the link

As mentioned above, the reference style of Markdown hyperlinking is preferred to the inline. Hyperlinks are marked with two pairs of square brackets, the first enclosing the hyperlinked text, the second enclosing a label for the link. Labels are in turn associated with a target URL in a list of declarations at the end of the document. Each label declaration consists of a line beginning with the bracket-enclosed label, a colon, and the target URL (the `href` in HTML). The target URL may optionally be followed by a link title in double quotes. The list of link label declarations should be sorted alphabetically.

#### Example: Reference-style hyperlinking

```markdown
The reference style of [Markdown hyperlinks][mdlinks] allows for easier
reading of source and formalizes the declaration of links.

Another paragraph may reference the [project introduction][readme],
which link will likewise have its label defined at the document's foot.

[mdlinks]: http://daringfireball.net/projects/markdown/syntax#link "Markdown link syntax"
[readme]: README.md
```

#### Relative URLs preferred

Using relative URLs where possible helps portability among multiple presentation targets, as they remain valid even as the site root moves. Absolute linking is obviously necessary for resources external to the document's repository and/or the Satyarat domains.

## Example: Documenting code blocks

Insert triple backtick (grave accent) characters on a new line before and after a block of code. A tag, such as `yaml`, `sh`, `json`, or `ini`, can be placed after the opening backticks to declare the language in the block. Markdown syntax is not interpreted within the gated code block, but special characters are replaced with HTML entities.

```yaml
apiVersion: v1
kind: Service
metadata:
 name: etcd-client
spec:
 ports:
 - name: etcd-client-port
   port: 2379
   protocol: TCP
   targetPort: 2379
 selector:
   app: etcd
```

View this document's source to see the Markdown that generates the code block above.

## File name extension conventions

Some file types are commonly identified with more than one file name extension. For example, YAML is usually stored in files whose names end in either `.yml`, or `.yaml`. For the sake of consistency, use the file name extension designated in the following list when referring to or creating files of any of the listed types in Satyarat projects and their documentation.

* YAML: `file.yaml` is preferred to `file.yml`
* HTML: `file.html`, not `file.htm`


[command-line-grammar]: #command-line-grammar
[eos]: https://faculty.washington.edu/heagerty/Courses/b572/public/StrunkWhite.pdf "The Elements of Style"
[githubmd]: https://help.github.com/articles/github-flavored-markdown/
[headings]: #headings
[hyperlink-considerations]: #hyperlink-considerations
[mdhome]: https://www.markdownguide.org
[rfc2606s3]: https://tools.ietf.org/html/rfc2606#section-3
[rfc5737]: https://tools.ietf.org/html/rfc5737
[style]: STYLE.md "Documentation Style and Formatting"
