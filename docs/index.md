---
template: main-index.html
---

<h1 id="welcometext"> Welcome to Docs CSC! </h1>

!!! Overview
    
    Docs CSC contains user guides, [FAQs](support/faq/index.md) and [tutorials](support/tutorials/index.md) related to CSC services.

    * In order to navigate across the CSC user guide, click on the topics on
      the left hand side of the navigation bar
    * Or use the search functionality


<h1 id="quicklinktitle"> Quick links </h1>


## Details

??? info "I'm hiding some content"
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.


## Tabbing

### MPI

=== "Mahti"
    ```
    #!/bin/bash
    #SBATCH --job-name=example
    #SBATCH --account=<project>
    #SBATCH --partition=medium
    #SBATCH --time=02:00:00
    #SBATCH --nodes=10
    #SBATCH --ntasks-per-node=128

    srun myprog <options>

    ```
=== "Puhti"
    ```
    #!/bin/bash
    #SBATCH --job-name=example
    #SBATCH --account=<project>
    #SBATCH --partition=large
    #SBATCH --time=02:00:00
    #SBATCH --ntasks=80
    #SBATCH --mem-per-cpu=4000

    srun myprog <options>
    ```
