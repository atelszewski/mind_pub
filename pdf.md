# Portable Document File (PDF)

## Resize margins

Left, bottom, right and top margins:

```
$ pdfjam --fitpaper true --trim "-1cm -1cm -1cm -1cm" \
      <input.pdf> -o <output.pdf>
```

## Split and merge

```
$ pdfseparate <input.pdf> <output-%d.pdf>
$ pdfunite <input-*.pdf> <output.pdf>
```
