source("renv/activate.R")

# Resolve conflicts
conflicted::conflict_prefer("filter", "dplyr", quiet = TRUE)
conflicted::conflict_prefer("select", "dplyr", quiet = TRUE)
conflicted::conflict_prefer("gather", "tidyr", quiet = TRUE)
conflicted::conflict_prefer("map", "purrr", quiet = TRUE)

# Return tibble from taxastand functions by default
options(ts_tbl_out = TRUE)