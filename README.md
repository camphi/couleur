# couleur
Bash tool to color output with regex

# Install
```shell
git clone --depth 1 https://github.com/camphi/couleur.git ~/.couleur
ln -s ~/.couleur/couleur ~/bin/
```

# Usage
```shell
Usage: command | couleur [global_options] [pattern_options]

Global Options:
  -u, --unbuffered              Flush output instantly (ideal for tail -f)
  -i, --ignore-case             Make all pattern matches case-insensitive
  -z, --null-data               Treat records as null-separated fields
  -f, --filter                  Only output lines that match at least one rule
  -p, --pristine                Force remove ANSI cntrl from stdin
  -h, --help                    Show this help block
  --                            Explicitly signals the end of global options

Pattern Options:
  -n, --negative <regex>        Highlight match using invert (Default)
  -r, --red <regex>             Highlight match in Bold Red
  -g, --green <regex>           Highlight match in Bold Green
  -y, --yellow <regex>          Highlight match in Bold Yellow

Standard Positional Syntax:
  <style_spec> <regex>          style_spec is a comma(",") delimited list of
                                color, background color, and modifiers. The
                                colours can be one of the 8 basic colors, or
                                a rgb code, or a hex-color.
                                regex is an ERE (Extended Regular Expression).
Ex:
tail -f var/log/system.log | couleur -u -f -r 'ERROR' -y 'WARNING'
cat /var/log/dpkg.log | couleur -r ' trigproc ' -y ' status ' -g ' configure '
parallel --tag-string server.{}.cloud -j0 ssh server.{}.cloud -ttt 'tail -f var/log/system.log' ::: {1..55} | couleur -u cyan '^[^\t]+\t' F54927,bg_rgb(238,245,39),bold ERREUR '\[[0-9]{4}-[0-9]{2}-[0-9]{2}[0-9 -:T]\+00:00\]'
```
