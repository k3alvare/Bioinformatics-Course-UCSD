Class 15 : Essential UNIX for Bioinformatics
================

``` r
b <- read.table("mm-second.x.zebrafish.tsv", col.names = c("qseqid", "sseqid", "pident", "length", "mismatch", "gapopen", "qstart", "qend", "sstart", "send", "evalue", "bitscore"))
```

``` r
## Asuming your blast results are stored in an object called 'b'
plot(b$pident  * (b$qend - b$qstart), b$bitscore)
```

![](Untitled_files/figure-gfm/unnamed-chunk-2-1.png)

``` r
library(ggplot2)
ggplot(b, aes(pident, bitscore)) + geom_point(alpha=0.1) 
```

![](Untitled_files/figure-gfm/unnamed-chunk-3-1.png)

``` r
ggplot(b, aes((b$pident * (b$qend - b$qstart)), bitscore)) + geom_point(alpha=0.1) + geom_smooth()
```

    Warning: Use of `b$pident` is discouraged.
    ℹ Use `pident` instead.

    Warning: Use of `b$qend` is discouraged.
    ℹ Use `qend` instead.

    Warning: Use of `b$qstart` is discouraged.
    ℹ Use `qstart` instead.

    Warning: Use of `b$pident` is discouraged.
    ℹ Use `pident` instead.

    Warning: Use of `b$qend` is discouraged.
    ℹ Use `qend` instead.

    Warning: Use of `b$qstart` is discouraged.
    ℹ Use `qstart` instead.

    `geom_smooth()` using method = 'gam' and formula = 'y ~ s(x, bs = "cs")'

![](Untitled_files/figure-gfm/unnamed-chunk-4-1.png)
