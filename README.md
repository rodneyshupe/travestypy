# Travesty in Python

This analyzes input text and then randomly generates text output based on the
pattern probability.

My first exposure to this algorithm was via a Pascal version published in
[BYTE November 1984](https://www.scribd.com/doc/99613420/Travesty-in-Byte)
([alt reference](https://archive.org/stream/byte-magazine-1984-11/1984_11_BYTE_09-12_New_Chips#page/n129/mode/2up)).
Since then I have implemented this algorithm as a learning tool for new
languages. Besides this implementation, I have done implementations in
*HP Basic*,
*Diabol*,
*Cobol*,
*PL1*,
*Plus*,
*C*,
*Visual Basic*,
*Java*,
*Perl*,
*Node.js*,
[*Bash*](https://github.com/rodneyshupe/travestysh),
[*Rust*](https://github.com/rodneyshupe/travestyrs),
and probably a few I have forgotten.

## Algorithm

This is a free interpretation of the Travesty algorithm by Hugh Kenner and
Joseph O'Rourke discussed in BYTE based on the paper
"[Richard A. O’Keefe - An introduction to Hidden Markov Models](www.cs.otago.ac.nz/cosc348/hmm/hmm.pdf)".

From this paper:
> A kth-order travesty generator keeps a “left context” of k symbols. Here
> k = 3, one context is “fro”. At each step, we find all the places in the
> text that have the same left context, pick one of them at random, emit the
> character we find there, and shift the context one place to the left. For
> example, the text contains “(fro)m”, so we emit “m” and shift the context
> to “rom”. The text contains “p(rom)ise”, so we emit “i” and shift the
> context to “omi”. The text contains “n(omi)nation”, so we emit “n” and shift
> the context to “min”. The text contains “(min)e”, so we emit “e” and shift
> the context to “ine”. And so we end up with “fromine”.
>
> How is this a Markov chain? The states are (k + 1)-tuples of characters,
> only those substrings that actually occur in our training text. By looking
> at the output we can see what each state was. There is a transition from
> state s to state t if and only if the last k symbols of s are the same as
> the first k symbols of t, and the probability is proportional to the number
> of times t occurs in the training text.
>
> A Travesty generator can never generate any (local) combination it has not
> seen; it cannot generalise"

## Getting Started

After cloning the repo you can quickly run with the following:
```sh
python3 travesty.py -- sample.txt
```

If you want to run with debugging on try the following:
```sh
python3 travesty.py -b 1000 -o 200 -d sample.txt
```

## Application Usage

Display usage message with `python3 travesty.py --help`

```
usage: travesty.py [-h] [-p [pattern_length]] [-b [buffer_size]]
                   [-o [out_size]] [-l [line_width]] [-d] [--verse] [-V]
                   [input_file]

Analyzes input text and then randomly generates text output based on the
pattern porbablity.

positional arguments:
  input_file            Sets the input file to use

optional arguments:
  -h, --help            show this help message and exit
  -p [pattern_length], --pattern-length [pattern_length]
                        Pattern Length
  -b [buffer_size], --buffer-size [buffer_size]
                        The size of the buffer to be analyzed. The larger this
                        is the slower the output will appear
  -o [out_size], --output-size [out_size]
                        Number of characters to output
  -l [line_width], --line-width [line_width]
                        Approximate line length to output
  -d, --debug           Print debugging info
  --verse               Sets output to verse mode, defaults to prose
  -V, --version         show program's version number and exit
```

## Attributions
* `sample.txt` - Extract of sonets from
  [bbejeck](https://github.com/bbejeck/hadoop-algorithms/blob/master/src/shakespeare.txt)'s
  *Complete Works of Shakespeare* text file.
* `adventure.txt` - Extract from Crowther, Will, and D. Woods.
  [Adventure](http://mirror.ifarchive.org/if-archive/games/source/adv350-pdp10.tar.gz)
  (aka "ADVENT" and "Colossal Cave") FORTRAN source code. 1977.
