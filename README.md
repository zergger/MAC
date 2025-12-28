# MAC2.0

MAC2.0 merges assemblies with an adjacency algebraic model and classification. It is a C++ refactor of the original MAC, fixes large-file handling, and removes the evaluation step that required raw reads.

Install **MUMmer 4.0** and make sure `nucmer`, `delta-filter`, and `show-coords` are in `PATH`. Versions lower than **MUMmer 4.0** will trigger errors. The source file is `MAC2.0.cpp` and it builds with `g++ -std=c++17 MAC2.0.cpp -o MAC2.0`.

Put the contig files in `./input` and run `./MAC2.0 <contig_query.fa> <contig_reference.fa>`. The program generates alignment intermediates in `./temp` and writes the final scaffold to `./output/scaffold.fasta`. The input, output, and temp folders are created automatically if they do not exist.

You can pass a thread count or custom `nucmer` arguments. The third argument is either an integer thread count or a single string of extra `nucmer` arguments. If a fourth argument is present, it is treated as the extra `nucmer` argument string. When the extra argument string contains spaces, wrap it in quotes.

```
./MAC2.0 q.fa r.fa
./MAC2.0 q.fa r.fa 8
./MAC2.0 q.fa r.fa "--maxmatch -l 100 -c 500 -t 10"
./MAC2.0 q.fa r.fa 8 "--maxmatch -l 100 -c 500"
```

Input filenames must end with `.fa`. If you need to merge more than two contig sets, merge them pairwise to produce intermediate results and then merge those results iteratively. Because of implementation limits, the final number of MAs may be slightly higher than the original approach.
