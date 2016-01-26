# Class notes for Non-Linear Optimization and Game Theory

- EIN 6935
- Spring 2016
- Dr. Changhyun Kwon
- <http://usflearn.instructure.com/courses/1089742>
- EDU 254: T/R 12:30 - 13:45

## Compile PDFs

Requires [pandoc].

```
lecture_notes=<filename_without_md_extension>
pandoc $lecture_notes.md -o $lecture_notes.pdf --latex-engine=xelatex --template=fancy.latex --highlight-style=tango
```

[pandoc]: http://johnmacfarlane.net/pandoc/
