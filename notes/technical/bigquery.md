
**datasets**
- a way of organizing big query resources
  - a way to control access
- tables, view, functions and procedures are created inside datasets
- datasets have locations, which can't be changed (you can copy the data to dataset in another project)
- datasets must exist within a project
- running queries or injesting/loading data create ***jobs***
  - jobs can belong projects outside of dataset's project
  - jobs must run inside the project associated with target dataset

- connections and jobs are associated with projects, not datasets
