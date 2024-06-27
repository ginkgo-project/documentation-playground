# `gko::experimental::distributed::Partition`

- vectors and matrices are row-wise distributed
- each row has an owning process
- represented by partition
  - image to show partition
- stored as collection of half-open intervals called ranges
- each range belongs to a part, i.e. process


## Creating

- multiple creation patterns supported
  - specify the part for each index
  - provide only ranges and part-ids
    - can leave out part-ids, then each range will belong to part-id same as range-id
  - uniform sizes for a given global size and number of parts
- partition can't be changed after created

### Helper Functions

- require communication
- each part specifies only its own size, global size and ranges are inferred
- each part specifies only its own range, ..., checks if no gaps globally

## Accessing 

- only const accessors
- scalar query functions
  - get_size
  - get_num_ranges
  - get_num_parts
  - get_num_empty_parts
- array query functions
  - compressed range bounds
  - range starting indices
  - part id per range
  - part size