# Isoform filtering.

To begin, the `.fasta` files of the extracted or publicly available proteomes were renamed in accordance with the KinFin documentation. This was also done in the `.gff` files of the annotations.

The following steps depend on the source of proteome data.

<details>
  <summary>From NCBI</summary>
  
  'Sanitise' proteins using `filter_fastas_before_clustering.py` (KinFin v1.0)
  E.g.
  ```
  ./filter_fastas_before_clustering.py \
  -f saccoglossus.saccoglossus_kowalevskii.faa > saccoglossus.saccoglossus_kowalevskii.filtered.faa
  ```
  
  Filter isoforms using `filter_isoforms_based_on_gff3.py.gff`
  
  ```
  ./filter_isoforms_based_on_gff3.py \
  -f saccoglossus.saccoglossus_kowalevskii.filtered.faa \
  -g gffs/saccoglossus.saccoglossus_kowalevskii.gff \
  -t NCBI
  ```
  
  ```
  grep -A1 -wFf saccoglossus.longest_isoforms.txt \
  saccoglossus.saccoglossus_kowalevskii.filtered.faa \
  > longest_isoforms/saccoglossus.saccoglossus_kowalevskii.filtered.longest.fa
  ```

</details>
